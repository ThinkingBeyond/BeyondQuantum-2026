![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Noise Analysis on GHZ-State Based Quantum Visual Secret Sharing (QVSS) in Medical Communication

***Provide a description of your project including*** 

1. motivating your research question
2. stating your research question
3. explaining your method and implementation
4. Briefly mention and discuss your results
5. Draw your conclusions
6. State what future investigations 
7. State your references 

### Further Guidance: Formating
- Structure this readme using subsections
- Your job is to 
    - keep it clear
    - provide sufficient detail, so what you did is understandable to the reader. This way other researchers and future cohorts of BeyondQuantum will be able to build on your research
    - List all your references at the end
- utilise markdown like *italics*, **bold**, numbered and unnumbered lists to make your document easier to read
- if you refer to links use the respective markdown for links, e.g. `[ThinkingBeyond](https://thinkingbeyond.education/)`
- If you have graphs and pictures you want to embed in your file use `![name](your_graphic.png)`
- If you want to present your results in a table use
    | Header 1            | Header 2  |
    |---------------------|-----------|
    | Lorem Ipsum         | 12345     |

**Tip:** Use tools to create markdown tables. For example, Obsidian has a table plugin, that makes creating tables much easier than doing it by hand.

## Motivation

Motivated by the relevance and significance of secure medical image sharing in existing healthcare systems, our research introduces a novel Entanglement-based Quantum Visual Secret Sharing (QVSS) scheme to encode binary pixel values directly into GHZ entangled states, enabling information-theoretic security.

Our project examines the limitations of existing medical image sharing approaches, presents the design and implementation of the proposed protocol, and evaluates its performance under state-level and gate-level noise to assess its practical robustness. 

## Medical Image Sharing 

Medical image sharing is frequently used in modern smart healthcare systems when patients obtain second opinions from external providers to inform treatment decisions. According to PubMed Central (2021), 79% of patients who consulted secondary opinions had a change in their treatment plans and reported better diagnoses. However, current healthcare infrastructure rely on a centralised Picture Archiving and Communications System (PACS) to store and distribute medical images containing patients’ personal data, medical scan and diagnosis which creates a single point of failure. 

A breach of the system could lead to ransom and exposure of patients’ data, whereas an attacker with write access could manipulate the images stored such as amending the doctor’s annotations, falsifying diagnoses and corrupting the images. 

## Classical Visual Secret Sharing (VSS)

Classical Visual Secret Sharing (VSS) was introduced to address this pitfall. VSS splits the original medical image into a number of random-like shares that contain no useful information when viewed individually. The image can only be reconstructed if a threshold number of shareholders cooperate. VSS schemes for binary images represent each pixel as a binary value (0 or 1) and map it into randomized subpixel patterns based on a predefined codebook. The original image is revealed only when a sufficient number of shares are combined, typically through stacking or XOR-based reconstruction with random masking. 

VSS decentralises authority and introduces an additional layer of security as compared to secure key distribution since it maintains security so long as the number of untrusted participants does not exceed the threshold number of shares required to reconstruct the image. 

However, because these schemes rely entirely on classical data, the shares can be freely copied and redistributed without intrinsic mechanisms for eavesdropping detection or tamper resistance. In addition, classical VSS often introduces pixel expansion and reduced contrast in reconstructed images, which can degrade visual quality and negatively impact diagnostic accuracy.

This illustrates the need for Quantum Visual Secret Sharing (QVSS), where quantum mechanics principles such as the No-Cloning theorem and Entanglement can resolve these drawbacks. 

## Research Question

Our research started with investigating existing quantum secret sharing protocols (such as HBB, KKI) and VSS protocols. We then investigated whether entanglement provided better security in VSS and looked into the noise channels and metrics we could use to evaluate the protocol’s performance. 

Hence, we have collapsed into the following research question:
How does GHZ-state based Quantum Visual Secret Sharing (QVSS) perform under noise in Medical Image Sharing? 


## Methodology and Implementation 

### Designing our Protocol

While researching existing QVSS schemes, we identified a meaningful gap. 

Many QVSS protocols incorporate quantum superposition and entanglement primarily for state preparation or quantum randomness, while the crucial security mechanisms remain largely classical. Particularly, several protocols rely on XOR-based operations or classical correlation after measurement to carry information and reconstruct the secret, limiting the role of quantum mechanics in encryption and transmission. We saw this as an opportunity to leverage intrinsic quantum properties in the security aspect of our novel QVSS protocol, where reconstruction of the secret depends on genuine quantum correlations instead of classical post-processing. 

To construct our protocol, we build upon the existing HBB(1999) quantum secret sharing protocol, the first ever secret sharing protocol to utilise GHZ-state entanglement for multi-party key distribution. A GHZ state is an entangled quantum state involving three qubits that exhibits perfect correlation in the computational basis, producing only fully aligned outcomes such as 000 or 111. The notation for a GHZ state is shown below: 

# IMAGE TO BE ADDED

By leveraging GHZ states, individual or partial measurements yield outcomes that appear random and provide no information about the global secret. Since our protocol involves three parties (Patient, Hospital A, Hospital B), this protocol’s methodology is ideal as a basis to our protocol since the secret can only be reconstructed if all parties cooperate by combining their respective shares. The key advantage we found from this approach lies in the fact that the secret is encoded and recovered through entanglement-based correlations rather than relying solely on classical correlation structures. 

Furthermore, the research area of QSS applications in imaging and medicine is relatively underdeveloped, motivating us to develop and evaluate a novel protocol built on quantum entanglement in secret reconstruction for this application area.

### Explaining the Novelty of our Protocol: 

1. Our protocol extends traditional GHZ-based quantum secret sharing into visual data encoding for imaging by directly encoding the binary image’s pixel values into the GHZ state rather than utilising entanglement only for key distribution or randomness generation.

2. Our protocol encodes (n-1) images simultaneously using a single n-qubit GHZ state, requiring only one GHZ triplet per pixel pair regardless of the number of images shared.

### Protocol Walkthrough
Our GHZ-3 protocol encrypts two binary images to be transmitted between three parties, namely the Patient (Authority), Hospital A (Secret Share 1) and Hospital B (Secret Share 2).

1. Pixels with the same index (i,j) in the respective binary images are paired together, such that (g{1,ij}, g{2,ij}) {0,1}2 .

2. Each pixel pair is encoded into a 3-qubit GHZ state (|GHZ⟩ = 12(|000⟩ + |111⟩) by applying the operation ,(I Xg1Xg2) ,such that the pixel values determine whether X-gate is applied on each qubit. The obtained GHZ state is shown below:
# IMAGE TO BE ADDED

3. Each GHZ state is measured to obtain results denoted as r0, r1, r2, to construct three share matrices held by each party participating in the transmission denoted as U, S1,S2 (whereby U is completely constructed of r0 values and vice versa).

4. Using the share matrices, each pixel from the secret images is reconstructed through the relation, g1,ij= ro,ijr1,ij  and g2,ij= ro,ijr2,ij.

5. Images are successfully reconstructed once the relation is applied to each pixel pair’s share matrices.

For the complete mathematical proof of the protocol, do refer to the LaTex document. 

### Protocol’s Performance at Zero Noise: 
The protocol was implemented in Python using Qiskit. Qiskit AER simulator was used to simulate the different noise channels. Results were measured using a range of metrics detailed in the noise robustness study section.

At Zero Noise, the protocol obtains perfect, lossless recovery of the two binary images across all noise channels tested (listed in Results section). The protocol’s performance in the following metrics are as follows: 
- BER = 0, PSNR = ∞, SSIM = 1.0
- Share entropy ≈ 1 bit/pixel, MI with secret ≈ 0 — no information leakage



Continue working through the points listed above with the help of sensibly named subsections. 



## Conclusion
The novel GHZ-3 QVSS protocol devised in this project addresses the security concerns and relevance in the application area of medical image sharing. By directly encoding the pixel values into the entangled GHZ state and encrypting two binary images simultaneously, we bridge the research gap in existing QVSS literature by introducing said novelty. 

Through testing against both state-level and gate-level noise, we observe the differences in thresholds, performance metrics and reconstructed images under both theoretical and realistic noise conditions. The protocol’s immunity to phase-flip under both types of noise is a key finding in regards to the protocol’s practicality and robustness on real networks, since existing fibre-optic networks are dominated by phase errors. 

## Future Work

Our future research will focus on improving the practicality and integration of the proposed protocol into existing healthcare infrastructure by redesigning it to operate in semi-quantum settings, where only hospitals are required to operate quantum hardware, and patients interact classically to address realistic infrastructure constraints. 

Additionally, the protocol will be extended from binary to grayscale image representations to support clinically relevant modalities such as MRI, CT, and X-ray scans to improve compatibility with existing DICOM workflows. 

## References

List all your references here. Remember to put links into markdown. For example:

1.  Einstein, A. (1905). *On the Electrodynamics of Moving Bodies*. Annalen der Physik, 17, 891-921. [Internet Archive](https://archive.org/details/einstein-1905-relativity)

**Tip**: *If you have you references in BibTex, Google Scholar or Zotero*
1. Create/copy a list into ChatGPT
2. Ask it to turn it into an unsorted list in markdown

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

