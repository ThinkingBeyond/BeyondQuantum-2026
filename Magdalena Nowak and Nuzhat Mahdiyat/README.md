![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Quantum Machine Learning for Exoplanet Classification

## Research Question

> *How does a hybrid quantum–classical feature extraction pipeline compare to classical models in the classification of Kepler KOI exoplanet data?*

- Specifically, we ask: can a quantum neural network (QNN) used as a feature extractor - feeding into a classical neural network - achieve competitive or superior classification performance compared to purely classical approaches such as Logistic Regression and a classical Multi-Layer Perceptron (MLP)?
---

## Motivation

- The NASA Kepler Mission has identified thousands of exoplanet candidates, but a significant fraction of detections are false positives caused by stellar noise or binary star systems. Reliably distinguishing confirmed exoplanets from false positives is a critical step in exoplanet science.
Classical machine learning methods have been applied to this task with strong results. However, Quantum Machine Learning (QML) offers a theoretically motivated alternative: quantum circuits operate in an exponentially large Hilbert space and can capture non-linear feature interactions that classical preprocessing methods like PCA inherently discard. This raises the question of whether quantum feature representations can provide a measurable advantage in classification accuracy on real astrophysical data.
---

## Data

We used the **Kepler Objects of Interest (KOI) Cumulative Table** from the [NASA Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu/).
 
- Each sample corresponds to one KOI
- **Label:** `1` = Confirmed exoplanet, `0` = False positive / non-planet
## Features (20 columns)

** Candidate disposition
| Feature | Description |
|---|---|
| `koi_score` | Disposition score (0–1); higher = more likely a planet |

** False positive flags
| Feature | Description |
|---|---|
| `koi_fpflag_ss` | Stellar eclipse — nearby eclipsing binary |
| `koi_fpflag_co` | Centroid offset — blended background source |
| `koi_fpflag_ec` | Ephemeris contamination — match with another object |
| `koi_fpflag_nt` | Non-transit shape — unusual light curve morphology |

** Transit geometry
| Feature | Description |
|---|---|
| `koi_period` | Orbital period [days] |
| `koi_time0bk` | Transit epoch [BJD − 2 454 833] |
| `koi_duration` | Transit duration [hours] |
| `koi_depth` | Transit depth [ppm] — fractional flux decrease |
| `koi_impact` | Impact parameter b — normalized distance from disk center |

** Planet properties
| Feature | Description |
|---|---|
| `koi_prad` | Planet radius [R⊕] — derived from transit depth |
| `koi_teq` | Equilibrium temperature [K] |
| `koi_insol` | Insolation flux [F⊕] — relative to Earth |

** Signal quality
| Feature | Description |
|---|---|
| `koi_model_snr` | Transit model fit SNR |
| `koi_tce_plnt_num` | TCE planet number — detection order in the system |

** Stellar parameters & sky position
| Feature | Description |
|---|---|
| `koi_steff` | Stellar effective temperature [K] |
| `koi_slogg` | Stellar surface gravity [log g] |
| `koi_kepmag` | Kepler-band magnitude [mag] |
| `ra` | Right ascension [°] |
| `dec` | Declination [°] |
 
A sample of the data:
 
| kepoi_name | kepler_name | koi_score |
|---|---|---|
| K00752.01 | Kepler-227 b | 1.0 |
| K00752.02 | Kepler-227 c | 0.969 |
| K00754.01 | — | 0.0 |
| K00755.01 | Kepler-664 b | 1.0 |
---

## Method & Implementation

### Overview of the Pipeline
 
```
Classical Features
       ↓
Preprocessing (Scaling + PCA)
       ↓
Quantum Circuit (U-gates + CX entanglement)
       ↓
Expectation Values ⟨Z⟩
       ↓
Classical Neural Network
       ↓
Binary Classification


```

Preprocessing :
- StandardScaler normalises all input features to zero mean and unit variance
- PCA (15 components, preserving ≥95% variance) reduces dimensionality
- MinMaxScaler rescales features to the range $[-\pi, \pi]$ for angle encoding into the quantum circuit.
The quantum component acts as a "feature transformation layer" - before classical learning.
 
- Encoding : Angle encoding via U-gates — each qubit encodes 3 features via rotation angles $(\theta, \phi, \lambda)$
- Entanglement : Circular CX (CNOT) connectivity — $q_0 \rightarrow q_1 \rightarrow \ldots \rightarrow q_4 \rightarrow q_0$
- Weights : Fixed random parameters $\theta \in [0, 2\pi]^5$ (no quantum training)
- Observables : Pauli-Z operators per qubit → 5-dimensional quantum feature vector $\langle Z_i \rangle$
- Framework : Qiskit `EstimatorQNN` with `StatevectorEstimator`
- Hilbert space dimension : $2^5 = 32$

The circuit architecture:
 
```
q₀: ─[U(x₀,x₁,x₂)]─●───────────────[Ry(θ₀)]─
q₁: ─[U(x₃,x₄,x₅)]─X─●─────────────[Ry(θ₁)]─
q₂: ─[U(x₆,x₇,x₈)]───X─●───────────[Ry(θ₂)]─
q₃: ─[U(x₉,x₁₀,x₁₁)]──X─●──────────[Ry(θ₃)]─
q₄: ─[U(x₁₂,x₁₃,x₁₄)]───X─●────────[Ry(θ₄)]─
```
### Models
Logistic Regression, trained on PCA-preprocessed features, serves as a lightweight global reference for what classical methods can achieve without any neural component. The Classical MLP - a two-layer feedforward network trained with Adam and Binary Cross-Entropy — is the more direct counterpart to the hybrid, since both share the same architecture; the only difference is that the hybrid receives the 5-dimensional quantum feature vector $\langle Z \rangle$ as input instead of PCA features, which makes the two directly comparable and isolates the effect of quantum feature extraction.

### Implementation
 
The full implementation is available in [`Final_Code.ipynb`](Final_Code.ipynb), written in Python using:
 
- [`Qiskit`](https://qiskit.org/) & `qiskit-machine-learning` - quantum circuit construction and QNN
- [`PyTorch`](https://pytorch.org/) - classical neural network
- [`scikit-learn`](https://scikit-learn.org/) - preprocessing, Logistic Regression, metrics
- [`pandas`](https://pandas.pydata.org/), [`matplotlib`](https://matplotlib.org/) - data handling and visualisation
---

## Results
 
All three models were evaluated on a held-out 20% test set. The table below reports five metrics: accuracy, F1, recall, precision, and AUROC (Area Under the Receiver Operating Characteristic Curve). AUROC measures how well a classifier separates the two classes across all possible decision thresholds — a value of 1.0 means perfect separation, 0.5 means random guessing. Because the KOI dataset is class-imbalanced, AUROC gives a more complete picture of performance than accuracy alone, capturing the trade-off between true positive rate and false positive rate regardless of threshold choice.
 
| Metric | LogReg | Classical MLP | Hybrid QNN-MLP |
|---|---|---|---|
| **Accuracy** | 0.9775 | 0.8933 | 0.8371 |
| **F1** | 0.9831 | 0.9249 | 0.8889 |
| **Recall** | 0.9915 | 0.9245 | 0.9915 |
| **Precision** | 0.9748 | 0.8603 | 0.8056 |
| **AUROC** | 0.9996 | 0.9924 | 0.9784 |
 
--Image of: ROC curve comparison of all three models  
--name: ROC_Comparison
---

### Discussion
 
- All three models achieved high recall (>0.99), confirming that exoplanet signals in Kepler KOI data are reliably detectable regardless of the approach used.
- Classical approaches outperformed the hybrid model on AUROC and precision. Logistic Regression, despite its simplicity, achieved the best overall scores - likely because the KOI dataset features are already highly engineered by NASA's pipeline.
- The hybrid model remained competitive, especially in recall, and its AUROC of 0.978 is still strong in absolute terms.
- The quantum component uses **fixed random weights** - no quantum training was performed. This is a known limitation: the QNN acts as a random feature map, not a trained encoder. Despite this, the extracted features proved informative enough for downstream classification.
---

## Future Work

The most impactful next steps, in order of priority:
 
- **Train the quantum weights (VQC):** The single most important follow-up. Replacing fixed random parameters with variational parameters optimised via gradient descent - making the quantum layer genuinely adaptive to the Kepler data - would likely close most of the performance gap with classical models.
- **Extend to raw Kepler light curves:** Moving beyond tabular KOI features to the raw photometric time series would expose far richer information. This requires more complex preprocessing (e.g. phase-folding, detrending) but is a natural and impactful next direction.
- **Test on real quantum hardware:** All results here come from a statevector simulator. Running the pipeline on real IBM Quantum hardware would introduce noise and decoherence effects, making robustness under realistic conditions an important open question to study.
- **Larger qubit systems and deeper circuits:** Scaling from 5 to more qubits, or adding data re-uploading layers, would increase the expressibility of the quantum feature map and is a natural architectural extension.
---

## References

1.  NASA Exoplanet Archive, California Institute of Technology. *Kepler Objects of Interest Cumulative Table*. [Online]. Available: [Kepler KOI Cumulative Table](https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=cumulative)
2. Bryson, S. T., et al. (2017). *The Kepler Certified False Positive Table*. KSCI-19093-003. NASA Ames Research Center. [Kepler False Positive Working Group](https://exoplanetarchive.ipac.caltech.edu)

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

