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
- **Features used (20 columns):**
| Feature | Description |
|---|---|
| `koi_score` | Disposition score |
| `koi_fpflag_ss`, `koi_fpflag_co`, `koi_fpflag_ec`, `koi_fpflag_nt` | False positive flags |
| `koi_period` | Orbital period |
| `koi_depth` | Transit depth |
| `koi_duration` | Transit duration |
| `koi_impact` | Impact parameter |
| `koi_prad` | Planet radius |
| `koi_teq` | Equilibrium temperature |
| `koi_insol` | Insolation flux |
| `koi_model_snr` | Model SNR |
| `koi_steff`, `koi_slogg`, `koi_kepmag` | Stellar parameters |
| `koi_tce_plnt_num` | TCE planet number |
| `koi_time0bk` | Transit epoch |
| `ra`, `dec` | Sky coordinates |
 
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

The circuit architecture:
 
```
q₀: ─[U(x₀,x₁,x₂)]─●───────────────[Ry(θ₀)]─
q₁: ─[U(x₃,x₄,x₅)]─X─●─────────────[Ry(θ₁)]─
q₂: ─[U(x₆,x₇,x₈)]───X─●───────────[Ry(θ₂)]─
q₃: ─[U(x₉,x₁₀,x₁₁)]──X─●──────────[Ry(θ₃)]─
q₄: ─[U(x₁₂,x₁₃,x₁₄)]───X─●────────[Ry(θ₄)]─
```

### Implementation
 
The full implementation is available in [`Final_Code.ipynb`](Final_Code.ipynb), written in Python using:
 
- [`Qiskit`](https://qiskit.org/) & `qiskit-machine-learning` - quantum circuit construction and QNN
- [`PyTorch`](https://pytorch.org/) - classical neural network
- [`scikit-learn`](https://scikit-learn.org/) - preprocessing, Logistic Regression, metrics
- [`pandas`](https://pandas.pydata.org/), [`matplotlib`](https://matplotlib.org/) - data handling and visualisation
---

## Results
 
All three models were evaluated on a held-out 20% test set. Key metrics:
 
| Metric | LogReg | Classical MLP | Hybrid QNN-MLP |
|---|---|---|---|
| **Accuracy** | 0.9775 | 0.8933 | 0.8371 |
| **F1** | 0.9831 | 0.9249 | 0.8889 |
| **Recall** | 0.9915 | 0.9245 | 0.9915 |
| **Precision** | 0.9748 | 0.8603 | 0.8056 |
| **AUROC** | 0.9996 | 0.9924 | 0.9784 |
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

