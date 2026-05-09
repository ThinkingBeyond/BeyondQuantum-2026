![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# QBER STABILITY IN MDI-QKD UNDER QUANTUM NOISE AND EAVESDROPPING 

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1bvzKuTybs4rG-iR4PXrXOz4z0rsHJXtD?usp=sharing)

## Research Question

How do different types of quantum noise (depolarising, phase damping, amplitude damping) and eavesdropping attacks affect the stability of the QBER in MDI-QKD, and to what extent can simple error correction strategies (such as repetition code and Hamming code) mitigate these effects to improve secure key generation?

## Key Terms and Definitions
#### Quantum Key Distribution (QKD):
A cryptographic method that uses quantum mechanics to allow two parties to securely generate a shared secret key.

#### Measurement-Device-Independent QKD (MDI-QKD):
A QKD protocol designed to eliminate detector-side attacks by introducing an untrusted intermediary (“Charlie”) who performs Bell-state measurements without learning the final key.

#### Quantum Bit Error Rate (QBER):
The percentage of bits received incorrectly during quantum communication. High QBER indicates either strong environmental noise, eavesdropping, or both.

#### Amplitude Damping Noise:
A noise channel representing energy loss, such as photon absorption, where quantum states decay from |1⟩ to |0⟩.

#### Phase Damping Noise (Dephasing):
A noise process that destroys quantum coherence without changing the energy state of the qubit.

#### Depolarising Noise:
A noise channel that randomly alters the quantum state, effectively acting as “white noise” in quantum systems.

#### Intercept-Resend Attack:
An eavesdropping strategy in which an attacker (Eve) measures transmitted qubits and sends replacement states, introducing detectable errors into the channel.

#### Quantum Error Correction (QEC):
Methods that protect quantum information from noise by encoding logical qubits into multiple physical qubits and correcting errors using syndrome measurements.

## Motivation

As quantum computing advances, many classical cryptographic systems are expected to become vulnerable to quantum attacks. This has increased the importance of quantum cryptography, particularly Quantum Key Distribution (QKD), which offers theoretically secure communication based on the laws of quantum mechanics.

Among QKD protocols, Measurement-Device-Independent QKD (MDI-QKD) is especially important because it removes detector-side vulnerabilities, one of the largest practical weaknesses in earlier protocols. However, even MDI-QKD remains highly sensitive to environmental noise, which can increase QBER and eventually prevent secure key generation altogether.

This project builds upon previous Beyond Quantum research conducted by Taskia Islam and Irene Gallini (2025), which compared multiple QKD protocols and identified noise sensitivity as a major limitation in practical quantum communication systems. Their findings motivated our decision to investigate how specific quantum noise channels and error correction strategies affect QBER stability in MDI-QKD.

More specifically, this research allowed us to:

- analyze how different quantum noise channels affect secure communication,
- investigate whether simple error correction methods can preserve security,
- explore how eavesdropping interacts with natural noise,
- and examine the limitations of classical post-processing compared to true quantum error correction.

These questions are directly connected to one of the central challenges of future quantum networks: not only reducing errors, but distinguishing natural noise from malicious interference.

## Methods Overview

Our investigation followed four connected phases, moving from understanding quantum noise to testing security under active attack.

Phase 1 modeled three major quantum noise channels in MDI-QKD using Qiskit simulations: amplitude damping (energy loss), phase damping (loss of coherence), and depolarizing noise (randomized states). We measured their impact on the Quantum Bit Error Rate (QBER) and Secret Key Rate (SKR) to identify which noise types most strongly threaten secure communication.

Phase 2 implemented a 3-qubit repetition code using quantum circuits and majority-vote decoding. This allowed us to test whether simple error correction could reduce QBER under realistic noisy conditions.

Phase 3 explored more advanced error correction through the Hamming [7,4,3] code and its quantum analogue, the Steane [[7,1,3]] code. We tested both matrix-based classical decoding and quantum circuit implementations with syndrome extraction, while also analyzing the practical challenges of fault-tolerant quantum error correction.

Phase 4 introduced an intercept-resend eavesdropping attack (“Eve”) to evaluate how noise, error correction, and active attacks interact in MDI-QKD security.

## Results and Analysis
### Phase 1 — Noise in MDI-QKD

Simulations showed that different noise channels affect MDI-QKD very differently.

Amplitude damping produced the highest QBER and the fastest collapse of secure communication, reaching 39.0% QBER at p = 0.30. Depolarizing noise showed similarly destructive behavior, while phase damping remained comparatively stable and never crossed the 11% security threshold within the tested range.

![QBER Across Noise Types](MDI-QKD_Raw_QBER_Across_Three_Noise_Types.png)

Because Secret Key Rate depends nonlinearly on QBER, small increases in error rapidly reduced secure key generation. Under amplitude damping, SKR nearly vanished by p ≈ 0.30, while phase damping still maintained usable key generation.

![SKR Across Noise Types](MDI-QKD_Secret_Key_Rate_Across_Three_Noise_Types.png)

Key finding:
MDI-QKD is most vulnerable to amplitude damping and depolarizing noise, while phase damping is significantly less destructive under Z-basis measurements.

These results justified focusing later correction strategies primarily on amplitude damping and depolarizing channels.

### Phase 2 — Repetition Code Error Correction

To reduce bit-flip dominated errors, we implemented a 3-qubit repetition code with majority-vote correction.

![phase](phase.png)

The repetition code significantly lowered error rates for amplitude damping and depolarizing noise. At p = 0.30:

Amplitude damping improved from 33.0% → 22.8% QBER
Depolarizing improved from 14.8% → 5.4% QBER

However, the code produced no improvement for phase damping because phase damping creates phase-flip (Z) errors rather than bit-flip (X) errors.

At high noise levels (p > 0.4), performance declined because multiple simultaneous qubit errors became common, exceeding the correction capability of the repetition code.

![repetition code](rep_code.png)

Key finding:
Simple repetition coding can substantially improve MDI-QKD reliability against bit-flip dominated noise, but fails completely against phase-flip errors.

### Phase 3 — Hamming and Steane Codes

To overcome the limitations of repetition coding, we explored the Hamming [7,4,3] code and the Steane [[7,1,3]] quantum code.

![hamming_code](hamming_code.png)

![steane_code](steane_code.png)

The classical Hamming decoder successfully identified single-bit errors through parity-check matrices. We then attempted a quantum implementation using syndrome extraction circuits and ancilla qubits.

Although the full Steane implementation did not function correctly, the process revealed several important challenges in practical quantum error correction:

- Correct logical state encoding
- Fault-tolerant syndrome extraction
- Ancilla crosstalk and residual entanglement
- Error propagation during stabilizer measurements

Despite implementation difficulties, Steane theoretically offers major advantages over repetition coding because it can detect both bit-flip and phase-flip errors.

Key finding:
The gap between theoretical quantum error correction and practical implementation is substantial, even for relatively small codes such as Steane [[7,1,3]].

### Phase 4 — Eavesdropping and the Masking Problem

Finally, we introduced an intercept-resend attack to test whether error correction could maintain secure communication under active eavesdropping.

![eve](eve.png)

QBER increased linearly with Eve’s attack probability, matching the theoretical relation:

QBER= 0.25p_eve + noise

The repetition code reduced QBER below the 11% security threshold for amplitude damping and depolarizing noise:

- Amplitude damping: 18.5% → 7.4%
- Depolarizing: 17.0% → 8.5%

However, phase damping remained above threshold at 13.0% because repetition codes cannot correct phase-flip errors.

This led to an important discovery: Eve masking.

Because the repetition code relies on measurement and majority voting, it behaves similarly to classical post-processing. As a result, Eve’s interference can become hidden inside the corrected noise floor, making attacks difficult to distinguish from natural channel noise.

Key finding:
Classical-style correction can lower QBER while simultaneously masking eavesdropping activity. True quantum error correction would be required to distinguish natural noise from malicious interference through syndrome analysis.

## Overall Conclusions

This project demonstrates that the effectiveness of quantum error correction depends strongly on the physical type of noise present in the channel.

Amplitude damping and depolarizing noise severely degrade MDI-QKD performance, but repetition coding can partially restore secure communication. Phase damping presents a fundamentally different challenge because it produces phase errors invisible to repetition-based correction.

Our exploration of Hamming and Steane codes showed that advanced quantum error correction could theoretically solve these limitations, but practical implementation remains highly complex due to fault-tolerance requirements.

Most importantly, our eavesdropping simulations revealed that lowering QBER alone is not sufficient for security. Classical-style correction may unintentionally conceal attacks within the natural noise floor, reinforcing the importance of true syndrome-based quantum error correction for future secure quantum networks.

## Future Work

This project showed that the effectiveness of quantum error correction depends strongly on the type of noise affecting the channel. While simple repetition codes improved performance against bit-flip dominated noise, they failed against phase-flip errors and introduced important security limitations such as Eve masking. Several promising directions remain open for future research.

One natural continuation would be implementing true fault-tolerant quantum error correction using codes such as the Steane code, Shor, or surface codes. Unlike repetition coding, these methods preserve superposition during correction and could potentially distinguish natural noise from malicious interference through syndrome analysis. However, they require significantly more advanced stabilizer measurements, ancilla management, and fault-tolerant circuit design.

Another important direction is phase-flip correction. Our results showed that repetition codes cannot correct phase damping because they only address bit-flip errors. Future groups could explore CSS-based constructions or dedicated phase-flip codes to improve security in dephasing-dominated quantum channels such as long-distance fiber communication.

Our eavesdropping simulations also revealed the masking problem: error correction may reduce QBER while simultaneously hiding Eve’s activity within the corrected noise floor. Future research could investigate whether syndrome statistics, machine learning, or hybrid quantum-classical analysis can identify attack patterns that remain invisible to classical post-processing alone.

A particularly interesting possibility involves hybrid quantum-classical correction systems. While classical codes already form the foundation of many quantum codes through the CSS construction, future work could explore how measured quantum communication data might interact with existing classical decoding infrastructure in practical communication networks. This could help reduce hardware costs and improve scalability, though major theoretical and security challenges remain unresolved.

Finally, future projects could extend this work beyond discrete-variable MDI-QKD toward continuous-variable MDI-QKD, which may offer higher key rates and stronger compatibility with modern telecommunications infrastructure, but introduces much greater mathematical and experimental complexity.

## References

* **Basak, N., & Paul, G. (2025).** Resource Reduction in Multiparty Quantum Secret Sharing of both Classical and Quantum Information under Noisy Scenario. *arXiv preprint arXiv:2504.16709*.
* **Eater, B. (2020).** *What is error correction? Hamming codes in hardware*. YouTube. [Link](https://www.youtube.com/watch?v=h0jloehRKas)
* **Fletcher, A. I., et al. (2025).** An overview of CV-MDI-QKD. *Reports on Progress in Physics*, 88, 084001. [DOI: 10.1088/1361-6633/adf4f4](https://doi.org/10.1088/1361-6633/adf4f4)
* **Gisin, N., Ribordy, G., Tittel, W., & Zbinden, H. (2002).** Quantum cryptography. *Reviews of Modern Physics*, 74(1), 145–195. [DOI: 10.1103/RevModPhys.74.145](https://doi.org/10.1103/revmodphys.74.145)
* **Joseph, D., et al. (2022).** Transitioning organizations to post-quantum cryptography. *Nature*. [DOI: 10.1038/s41586-022-04623-2](https://doi.org/10.1038/s41586-022-04623-2)
* **Mermin, N. D.** *Quantum Computer Science: An Introduction*.
* **Preskill, J.** *Quantum Computing (CST Part II)*. University of Cambridge. [Link](https://www.cl.cam.ac.uk/teaching/1920/QuantComp/Quantum_Computing_Lecture_13.pdf)
* **Sanderson, G. [3Blue1Brown]. (2020).** *How to send a self-correcting message*. YouTube. [Link](https://www.youtube.com/watch?v=X8jsijhllIA)
* **Sanderson, G. [3Blue1Brown]. (2020).** *Hamming codes part 2, the elegance of it all*. YouTube. [Link](https://www.youtube.com/watch?v=b3NxrZOu_CE)
* **Shahid, A. B., et al. (2026).** Post-quantum cryptographic authentication protocol for industrial IoT using lattice-based cryptography. *Scientific Reports*, 16, 9582. [DOI: 10.1038/s41598-025-28413-8](https://doi.org/10.1038/s41598-025-28413-8)
* **Shi, S., et al. (2026).** Towards Minimal Fault-tolerant Error-Correction Sequence with Quantum Hamming Codes. *arXiv preprint arXiv:2601.10042*.
* **Subramani, S., et al. (2025).** Review of security methods based on classical cryptography and quantum cryptography. *Cybernetics and Systems*, 56(3), 302–320. [DOI: 10.1080/01969722.2023.2166261](https://doi.org/10.1080/01969722.2023.2166261)
* **Sun, Y., et al. (2025).** Analyzing the performance of CV-MDI QKD under continuous-mode scenarios. *Physical Review Applied*, 23, 014056. [DOI: 10.1103/PhysRevApplied.23.014056](https://doi.org/10.1103/PhysRevApplied.23.014056)
> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

