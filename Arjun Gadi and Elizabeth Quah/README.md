![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# **Noise Analysis on Novel GHZ-State Based Quantum Visual Secret Sharing in Medical Communication**

---

## **Motivation**  
Motivated by the relevance and significance of secure medical image sharing in existing healthcare systems, our research introduces a novel Entanglement-based Quantum Visual Secret Sharing (QVSS) scheme to encode binary pixel values directly into GHZ entangled states, enabling information-theoretic security.

Our project examines the limitations of existing medical image sharing approaches, presents the design and implementation of the proposed protocol, and evaluates its performance under state-level and gate-level noise to assess its practical robustness. 

---

## **Medical Image Sharing**
Medical image sharing is frequently used in modern smart healthcare systems when patients obtain second opinions from external providers to inform treatment decisions. According to PubMed Central (2021), 79% of patients who consulted secondary opinions had a change in their treatment plans and reported better diagnoses. However, current healthcare infrastructure rely on a centralised Picture Archiving and Communications System (PACS) to store and distribute medical images containing patients’ personal data, medical scan and diagnosis which creates a single point of failure. 

A breach of the system could lead to ransom and exposure of patients’ data, whereas an attacker with write access could manipulate the images stored such as amending the doctor’s annotations, falsifying diagnoses and corrupting the images. 

---

## **Classical VSS**
Classical Visual Secret Sharing (VSS) was introduced to address this pitfall. VSS splits the original medical image into a number of random-like shares that contain no useful information when viewed individually. The image can only be reconstructed if a threshold number of shareholders cooperate. VSS schemes for binary images represent each pixel as a binary value (0 or 1\) and map it into randomized subpixel patterns based on a predefined codebook. The original image is revealed only when a sufficient number of shares are combined, typically through stacking or XOR-based reconstruction with random masking. 

VSS decentralises authority and introduces an additional layer of security as compared to secure key distribution since it maintains security so long as the number of untrusted participants does not exceed the threshold number of shares required to reconstruct the image. 

However, because these schemes rely entirely on classical data, the shares can be freely copied and redistributed without intrinsic mechanisms for eavesdropping detection or tamper resistance. In addition, classical VSS often introduces pixel expansion and reduced contrast in reconstructed images, which can degrade visual quality and negatively impact diagnostic accuracy.

This illustrates the need for Quantum Visual Secret Sharing (QVSS), where quantum mechanics principles such as the No-Cloning theorem and Entanglement can resolve these drawbacks. 

---

## **Research Question**

Our research started with investigating existing quantum secret sharing protocols (such as HBB, KKI) and VSS protocols. We then investigated whether entanglement provided better security in VSS and looked into the noise channels and metrics we could use to evaluate the protocol’s performance. 

Hence, we have collapsed into the following research question:

1. How does GHZ-state based Quantum Visual Secret Sharing (QVSS) perform under noise in Medical Image Sharing? 

---

## **Methodology and Implementation**

### **Designing our Protocol**
  
While researching existing QVSS schemes, we identified a meaningful gap. 

Many QVSS protocols incorporate quantum superposition and entanglement primarily for state preparation or quantum randomness, while the crucial security mechanisms remain largely classical. Particularly, several protocols rely on XOR-based operations or classical correlation after measurement to carry information and reconstruct the secret, limiting the role of quantum mechanics in encryption and transmission. We saw this as an opportunity to leverage intrinsic quantum properties in the security aspect of our novel QVSS protocol, where reconstruction of the secret depends on genuine quantum correlations instead of classical post-processing. 

To construct our protocol, we build upon the existing HBB(1999) quantum secret sharing protocol, the first ever secret sharing protocol to utilise GHZ-state entanglement for multi-party key distribution. A GHZ state is an entangled quantum state involving three qubits that exhibits perfect correlation in the computational basis, producing only fully aligned outcomes such as 000 or 111\. The notation for a GHZ state is shown below: 

- ![](image1.png)

The quantum circuit required to construct a GHZ state is shown below: 

- ![](image2.png)

([https://en.wikipedia.org/wiki/Quantum\_secret\_sharing](https://en.wikipedia.org/wiki/Quantum_secret_sharing) )

By leveraging GHZ states, individual or partial measurements yield outcomes that appear random and provide no information about the global secret. Since our protocol involves three parties (Patient, Hospital A, Hospital B), this protocol’s methodology is ideal as a basis to our protocol since the secret can only be reconstructed if all parties cooperate by combining their respective shares. The key advantage we found from this approach lies in the fact that the secret is encoded and recovered through entanglement-based correlations rather than relying solely on classical correlation structures. 

Furthermore, the research area of QSS applications in imaging and medicine is relatively underdeveloped, motivating us to develop and evaluate a novel protocol built on quantum entanglement in secret reconstruction for this application area.

---

### **Explaining the Novelty of our Protocol**

1. Our protocol extends traditional GHZ-based quantum secret sharing into visual data encoding for imaging by directly encoding the binary image’s pixel values into the GHZ state rather than utilising entanglement only for key distribution or randomness generation.

2. Our protocol encodes (n-1) images simultaneously using a single n-qubit GHZ state, requiring only one GHZ triplet per pixel pair regardless of the number of images shared. 

---

### **Protocol Walkthrough**
Our GHZ-3 protocol encrypts two binary images to be transmitted between three parties, namely the Patient (Authority), Hospital A (Secret Share 1\) and Hospital B (Secret Share 2).

1. Pixels with the same index (i,j) in the respective binary images are paired together, such that (g{1,ij}, g{2,ij}) {0,1}2 .

2. Each pixel pair is encoded into a 3-qubit GHZ state (|GHZ⟩ \= 12(|000⟩ \+ |111⟩) by applying the operation ,(I Xg1Xg2) ,such that the pixel values determine whether X-gate is applied on each qubit. The obtained GHZ state is shown below:

![](image3.png)

3. Each GHZ state is measured to obtain results denoted as r0, r1, r2, to construct three share matrices held by each party participating in the transmission denoted as U, S1,S2 (whereby U is completely constructed of r0 values and vice versa).

4. Using the share matrices, each pixel from the secret images is reconstructed through the relation, g1,ij= ro,ijr1,ij  and g2,ij= ro,ijr2,ij. 

5. Images are successfully reconstructed once the relation is applied to each pixel pair’s share matrices. 

For the complete mathematical proof of the protocol, do refer to the LaTex document. 

---

## **Protocol’s Performance at Zero Noise**

The protocol was implemented using Qiskit 

At Zero Noise, the protocol obtains perfect, lossless recovery of the two binary images across all noise channels tested (listed in Results section). The protocol’s performance in the following metrics are as follows: 

* BER \= 0, PSNR \= ∞, SSIM \= 1.0  
* Share entropy ≈ 1 bit/pixel, MI with secret ≈ 0 — no information leakage

---

## **Noise Robustness Study**

To evaluate the robustness of this novel GHZ-3 protocol, we tested the protocol against four different noise channels:

1. **Depolarizing Channel**: The "all-directions" noise model. With probability λ, the qubit is completely randomised.  
- **Important:** In Qiskit, the depolarizing noise parameter λ is not the same as the standard Pauli error probability p. Instead, they are related by p \= 34λ. All results in our research project are consistently computed using λ (Qiskit convention).

2. **Bit-Flip Channel**: This channel applies an X gate (flips |0⟩↔|1⟩) with probability p. 

3. **Phase-Flip Channel**: This channel applies a Z gate (flips the sign: |1⟩→−|1⟩) with probability p. 

4. **Amplitude Damping**: This channel models energy relaxation such that the qubit spontaneously decays from |1⟩ to |0⟩ with probability γ.This is the most physically realistic channel for superconducting qubits.

---

### **Noise Modes**

1. State-Level Noise (Mode A): Apply the noise channel once to each qubit of the final prepared state, without involving gates at all. This is what the analytical formulas calculate. These analytical formulas can be found in fig12\_analytical.png    
2. Gate-Level Noise (Mode B): In Qiskit, a noise channel is attached to specific gate operations. Every time that gate fires, the error is applied. 
While standard analytical models often rely on the effect of noise on the final prepared state of the qubit, this study implements a dual-mode noise characterization. By comparing idealised state-level errors, against instruction-level gate errors, we identify the specific threshold where standard analytical predictions fail to reflect the decoherence reality of NISQ-era hardware. 

---

### **Metrics**

To quantify the results of this study, we used a range of metrics. The following table details the important metrics. 

| Fidelity | Measures how closely an actual quantum state matches the ideal state, on a range of 0 to 1\. A value below 0.5 would indicate that the quantum advantage is lost completely. |
| :---- | :---- |
| Bit Error Rate (BER)  | The fraction of bits (pixels) that are incorrectly reconstructed.  BER=0 means perfect recovery. BER=0.5 means the output is completely random. |
| SSIM (Structural Similarity Index) | Measures perceptual similarity between two images on a scale from −1 to 1\. SSIM=1 means identical. SSIM≈0 means no structural similarity. |
| Mutual Information I(S;G) | Measures how much information shared by S reveals about secret G. |

---

## **Plot analysis**

### **Heatmap**

![](image4.png)

The above plot shows a heatmap for the fidelity values obtained when the noise level is manipulated for the 4 noise channels. Bit-flip noise shows the sharpest degradation, and collapses at p ≈ 0.25. With depolarising noise fidelity drops below F=0.5 at λ ≈ 0.30. Amplitude damping is most resilient. 

---

### **Fidelity comparison**

![](image5.png)

The above plot illustrates the difference in fidelity between Mode A and Mode B. Mode A gives the theoretical floor, which matches the analytical formulas exactly, while Mode B reflects the nature of real IBM hardware. Mode B consistently performs worse than Mode A, the gap between them is the implementation overhead. 

---

### **BER**

![](image6.png)

As expected, as the noise increases the BER increases. However, the remarkable result here is the impact of Phase-Flip noise on BER. As illustrated in the graph, the protocol is immune to phase flip noise. This is significant because real life fibre optic quantum channels are dominated by phase errors, suggesting that GHZ-3 QSS may be more robust on real network than bit-flip based analysis would predict. 

---

### **Visual reconstruction**

![](image7.png)

The above plot shows the impact on the reconstructed image as the level of depolarising noise increases. Consistent with the BER plot, as the depolarising parameter increases, the quality of the reconstructed image decreases. While depolarising, bit-flip, and amplitude damping all degrade the reconstructed image, it is important to note that under phaseflip noise, the reconstructed image would be the exact same as the original image.

---

## **Comparison against Classical VSS**

| Property | Classical VSS | GHZ3 Protocol |
| :---- | :---- | :---- |
| Qubit/Bit Cost per Pixel | The cost scales with expansion factor | A fixed ratio of 2 bits per 3 qubits; no expansion |
| Multi-Image Capacity | Sharing two images requires two separate protocol runs | Single 3-qubit GHZ triplet simultaneously encodes two pixel pairs; generalizes to n-qubit GHZ encoding n-1 images |
| Threshold  | Tunable (k,n) threshold; any k of n shares suffice;  | (n,n) threshold; all n parties required to reconstruct shares. |
| Quantum Requirements | None; purely classical | Requires: quantum entanglement, qubit distribution/measurement, or quantum channel; sensitive to decoherence and gate noise |
| Individual Share Appearance | Each classical share is visually degraded/noisy; individual share reveals partial visual information. | Each quantum share rₖ ∈ {0,1} is uniformly random; no visual information leaked. |

---

## **Conclusion**
The novel GHZ-3 QVSS protocol devised in this project addresses the security concerns and relevance in the application area of medical image sharing. By directly encoding the pixel values into the entangled GHZ state and encrypting two binary images simultaneously, we bridge the research gap in existing QVSS literature by introducing said novelty. 

Through testing against both state-level and gate-level noise, we observe the differences in thresholds, performance metrics and reconstructed images under both theoretical and realistic noise conditions. The protocol’s immunity to phase-flip under both types of noise is a key finding in regards to the protocol’s practicality and robustness on real networks, since existing fibre-optic networks are dominated by phase errors. 

---

## **Future Work**
Our future research will focus on improving the practicality and integration of the proposed protocol into existing healthcare infrastructure by redesigning it to operate in semi-quantum settings, where only hospitals are required to operate quantum hardware, and patients interact classically to address realistic infrastructure constraints. 

Additionally, the protocol will be extended from binary to grayscale image representations to support clinically relevant modalities such as MRI, CT, and X-ray scans to improve compatibility with existing DICOM workflows. 

---

## **References**


Aolita, L., R. Chaves, D. Cavalcanti, A. Acín, and L. Davidovich. "Scaling Laws for the Decay of Multiqubit Entanglement." *Physical Review Letters* 100 (2008): 080501\. arXiv:0801.1305.

Basak, M., and P. Paul. "Resource Reduction in Multiparty Quantum Secret Sharing of Both Classical and Quantum Information Under Noisy Scenario." arXiv:2504.16709 (2025).

Hillery, M., V. Bužek, and A. Berthiaume. "Quantum Secret Sharing." *Physical Review A* 59, no. 3 (1999): 1829\. arXiv:quant-ph/9806063.

Imai, H., J. Müller-Quade, A. C. A. Nascimento, P. Tuyls, and A. Winter. "A Quantum Information Theoretical Model for Quantum Secret Sharing Schemes." arXiv:quant-ph/0311136 (2003).

Liu, W., Y. Xu, J. Chen, and C.-N. Yang. "A Novel Quantum Visual Secret Sharing Scheme." arXiv:2309.13659 (2023).

Musanna, F., and S. Kumar. "A Novel Three-Party Quantum Secret Sharing Scheme Based on Bell State Sequential Measurements with Application in Quantum Image Sharing." *Quantum Information Processing* 19 (2020): 348\. arXiv:2008.06228.

Nielsen, M. A., and I. L. Chuang. *Quantum Computation and Quantum Information*. Cambridge University Press, 2000\.

Qin, H., R. Gao, H. Wen, and Z. Zhu. "Cryptanalysis of the Hillery-Bužek-Berthiaume Quantum Secret-Sharing Protocol." *Physical Review A* 76 (2007): 062324\. arXiv:0801.2418.

Qiskit Aer Documentation. Depolarizing Error API. Accessed April 2026\. [https://qiskit.github.io/qiskit-aer/](https://qiskit.github.io/qiskit-aer/).

Rabari, D. K., Y. K. Meghrajani, and L. S. Desai. "Universal Share-Based Quantum Multi-Secret Image Sharing Scheme." arXiv:2509.12979 (2025).

Ray, M., R. Chatterjee, and I. Chakrabarty. "Sequential Quantum Secret Sharing in a Noisy Environment Aided with Weak Measurements." arXiv:1402.2383 (2016).

"Secret Sharing." Wikipedia. Accessed May 4, 2026\. [https://en.wikipedia.org/wiki/Secret\_sharing](https://en.wikipedia.org/wiki/Secret_sharing).

Sharma, Th., A. Thapliyal, A. Pathak, and S. Banerjee. "A Comparative Study of Protocols for Secure Quantum Communication Under Noisy Environments." arXiv:1603.00178 (2016).

Simon, A. K., and L. Kempe. "Robustness of Multipartite Entanglement." arXiv:quant-ph/0109102 (2002).

"Quantum Secret Sharing." Wikipedia. Accessed May 4, 2026\. [https://en.wikipedia.org/wiki/Quantum\_secret\_sharing](https://en.wikipedia.org/wiki/Quantum_secret_sharing).

Ignore this   
If you want to see some good examples of README files check out:  
- [Example 1](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/warenya-loulia/README.md)  
- [Example 2](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/shaana-karuna/README.md)  

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).
