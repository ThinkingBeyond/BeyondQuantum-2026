![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# QBER STABILITY IN MDI-QKD UNDER QUANTUM NOISE AND EAVESDROPPING 

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1hMkjwqCfdoX6ONX73SsGv-NObnIk8L6w?usp=sharing)

## Sections of this document
- The research question
- Why we chose this topic
- The keywords
- the key words  - simplified definitions
- A comparative analysis of three quantum noise channels in Measurement-Device-Independent Quantum Key Distribution (understanding the problem)
- An implementation of a 3-qubit repetition code for noisy quantum channels (the simple fix)
- The exploration of classical Hamming decoding and Steane-style quantum error correction challenges (The more complex fix)
- An Analysis of QBER stability under intercept-resend attacks (further testing)
- The future areas of research based on our findings
- Our references

## Research Question

How do different types of quantum noise (depolarising, phase damping, amplitude damping) and eavesdropping attacks affect the stability of the QBER in MDI-QKD, and to what extent can simple error correction strategies (such as repetition code and Hamming code) mitigate these effects to improve secure key generation?


## Motivation

As Quantum computing and, therefore, quantum communication advance and become more widespread, the need for secure communication will only increase. Once it is implemented into critical infrastructure, such as hospitals for medical imaging, as seen in one of the other groups in the cohort, secure quantum communication will become more than just a preference; it will be a requirement. This has led to developments in quantum communication algorithms, such as BB84 and E91, as Askia Isla and Irene Gallini found in their project last year on this topic. However, both of those have severe limitations in practical applications, which is why MDI-QKD was created. This algorithm uses Bell-state measurements and introduces a third party into the equation, thereby making the communication between A and B secure.


However, measurement-device-independent quantum key distribution is vulnerable to noise. Increasing the noise to make the quantum bit error rate above 11%, and the whole algorithm stops functioning. This means that whilst in theory, MDI QKD is secure, in practise, the real-world noise it faces is a major problem. Hence, this year we decided to dedicate our project to address this real-world issue, to make the algorithm usable.

To approach this problem realistically, we modelled three major quantum noise channels (amplitude damping, phase damping, and depolarising noise) using Qiskit simulations, and then analysed how both error correction and eavesdropping attacks affected the QBER and the Secret Key Rate (SKR). Instead of immediately relying on highly theoretical fault-tolerant quantum codes that remain difficult to implement on modern hardware, we first explored simpler, more practical correction methods, such as repetition coding and Hamming-based techniques, to evaluate the improvements realistically achievable in near-term quantum systems.


## Key Terms and Definitions shown in this research (advanced)
#### Quantum Key Distribution:
A cryptographic method that uses quantum mechanics to allow two parties to securely generate a shared secret key. 
#### Measurement-Device-Independent QKD (MDI-QKD):
A QKD protocol designed to eliminate detector-side attacks by introducing an untrusted intermediary (“Charlie”) who performs Bell-state measurements without learning the final key. Currently, it is amongst the most secure quantum cryptography algorithms, significantly better than E91 or BB84. 
#### Quantum Bit Error Rate (QBER):
The percentage of bits received incorrectly during quantum communication. High QBER indicates either strong environmental noise, eavesdropping, or both. 
#### Amplitude Damping Noise:
A noise channel representing energy loss, such as photon absorption, where quantum states decay from |1⟩ to |0⟩. 
#### Phase Damping Noise (Dephasing):
A noise process that destroys quantum coherence without changing the energy state of the qubit. 
#### Depolarising Noise:
A noise channel that randomly alters the quantum state in quantum systems. 
#### Intercept-Resend Attack:
An eavesdropping strategy in which an attacker (Eve) measures transmitted qubits and sends replacement states, introducing detectable errors into the channel. 
#### Quantum Error Correction (QEC):
Methods that protect quantum information from noise by encoding logical qubits into multiple physical qubits and correcting errors using syndrome measurements. 
#### Secure Key Rate (SKR):
A measure of how successful the key generation is. 

## Key Terms and Definitions shown in this research (simple)
#### Quantum Key Distribution: 
Think of it like a password that is secret - so only A and B can communicate - no one else can join in.

#### Measurement-Device-Independent QKD (MDI-QKD):
It's the best "key" version generator we have.

#### Quantum Bit Error Rate (QBER):
It's a measure of how successful the communication between A and B is in terms of % or as a decimal from 0 to 1

#### Amplitude Damping Noise:
We can think of this as the loss of energy - the photons just stop there.

#### Phase Damping Noise (Dephasing):
This is where the superposition gets removed - it stops being quantum.

#### Depolarising Noise:
We can think of this as white noise / static - it's just random. 

#### Intercept-Resend Attack:
This is because when we measure something in quantum mechanics, we remove information about it.

#### Quantum Error Correction (QEC):
It deals with the noise, so it's no longer such a big issue.

#### Secure Key Rate (SKR):
How often that password that we talked about earlier is generated correctly.


##  Research phases summarised

Our investigation followed four connected phases, moving from understanding quantum noise to testing security under active attack.

In Phase 1, we modelled three major quantum noise channels in MDI-QKD using Qiskit simulations: amplitude damping (energy loss), phase damping (loss of coherence), and depolarising noise (randomised states). We measured their impact on the Quantum Bit Error Rate (QBER) and Secret Key Rate (SKR) to identify which noise types most strongly threaten secure communication.

In Phase 2, we implemented a 3-qubit repetition code using quantum circuits and majority voting. We wanted to solve the noise as easily as possible.

In Phase 3, we explored more advanced error correction through the Hamming [7,4,3] code and its quantum analogue, the Steane [[7,1,3]] code. We went through every single version of Hamming code, and in the end, we managed to get the circuit-based approach and the matrix-based approach working. We also attempted to create a translator for quantum data to input it into the simpler classical algorithm, which led to an interesting discovery. However, due to time-based limitations, we only managed to get the aforementioned 2 to work. 

In Phase 4, we introduced an intercept-resend eavesdropping attack (“Eve”) to evaluate how noise, error correction, and active attacks interact in MDI-QKD security.

## Results and Analysis
### Phase 1 — Noise in MDI-QKD

We ran 3 simulations, which showed that different noise channels affect MDI-QKD very differently.


Amplitude damping produced the highest QBER and the fastest collapse of secure communication, 
Its QBER was 39.0% at p = 0.30, where p is the noise probability.

Depolarising noise showed similarly destructive behaviour, but its curve was slightly gentler, 

Phase damping remained comparatively stable and only crossed the 11% security threshold within the tested range at the very end. 

![QBER Across Noise Types](MDI-QKD_Raw_QBER_Across_Three_Noise_Types.png)

Because the secret key rate depends nonlinearly on QBER, small increases in the error rate reduce the  secure key generation rapidly. Under amplitude damping, SKR nearly vanished by p ≈ 0.30, while phase damping still maintained usable key generation until the very end.

![SKR Across Noise Types](MDI-QKD_Secret_Key_Rate_Across_Three_Noise_Types.png)

Main takeaway for this section of the research:
MDI-QKD is most vulnerable to amplitude damping, followed by depolarising noise, while phase damping is significantly less impactful, so we decided to focus less on it going forward. 


### Phase 2 — Repetition Code Error Correction

To reduce bit-flip-dominated errors, we implemented a 3-qubit repetition code with majority-vote correction.
This works by copying each transmitted bit 3 times, then checking the bits which arrive in series of 3. The bit which comes up the most is taken to be correct. However, if there are multiple of 2 errors, then it cannot be detected. Also, it increases the number of bits we have to transmit. It triples the data size
![phase](phase.png)
![amplitude](amplitude.png)

The repetition code significantly lowered error rates for amplitude damping and depolarising noise. At p = 0.30 for both of them (same as before):

Amplitude damping started at 33.0%, and it is now at 22.8% for the QBER
Depolarising started at  14.8%, and it is now at  5.4% for the QBER

However, the code showed no improvement in phase damping as we implemented it to correct the qubit value, not its phase, due to the extra time required for that.

At high noise levels (p > 0.4), a multiple of 2n errors is very common, meaning that the results became much less reliable.

![repetition code](rep_code.png)

Main takeaway for this section of the research:
While it reduces the error rate for bit flip errors, the data transmitted is 3x more, and if there are 2n errors, it still fails.

### Phase 3 — Hamming and Steane Codes

To overcome the limitations of repetition codes, we explored the Hamming [7,4,3] code and the Steane [[7,1,3]] quantum code.
The Hamming code was invented by John Hamming, who worked on the Manhattan Project, and it's a much more refined way of detecting errors and correcting them in $log_2 (n) +1$ bits. It arranges the data into a logical matrix and calculates the parity bits for each row and column, which is to say that it counts the number of 1s in a row/ column. If there is a mismatch, the parity bits can be used to give the exact placement of the error within the matrix, and therefore, it can correct it.


![hamming_code](hamming_code.png)


During this phase, we attempted all of the implementation methodologies, including the matrix-based, the circuit-based, the XOR-based and more. We found that in order to convert the classical Hamming code to work with quantum data, we would need a quantum data-to-classical algorithm translator (see future work section). We eventually settled on the circuit-based approach and Steane code for the matrix-based approach, which can detect both bit and phase flip errors, without having to create 2 seperate versions of it. The QBER was also lower compared to the repetition code, meaning that it is more applicable to the 2 algorithms
 

Main takeaway for this section of the research:
Despite the working algorithm, due to hardware limitations, the real-world applicability of Steane code is limited for the time being.

### Phase 4 — Eavesdropping and the Masking Problem

Due to the problematic nature of eavesdropping for quantum communication, it destroys the data that it reads. We decided to test how QBER is impacted by eavesdropping and whether the implemented repetition code could mitigate these effects.

![eve](eve.png)

The QBER increased linearly with Eve’s attack probability, matching our prediction of what the relationship should be in theory.


The repetition code reduced QBER below the 11% security threshold for amplitude damping and depolarising noise:

- Amplitude damping started at 18.5%, and it is now at 7.4% for the QBER
- Depolarising started at 17.0%, and it is now at 8.5% for the QBER

However, phase damping remained above threshold at 13.0% because our implementation of the repetition code does not correct phase-flip errors, as we were time-constrained.

This led to the realisation of Eve masking.


The eavesdropper could be hidden by the noisy environment and could be hidden even in the corrected code at the receiver.

Main takeaway for this section of the research:
The correction mechanisms that we have implemented reduce how the message is impacted by noise. However, they also allow for eavsedropping to be hidden, meaning that another method of error correction should be developed and looked into (see future work)

## Conclusions

The type of noise present in a system greatly impacts the error rate and the effectiveness of any correction algorithms.

Amplitude damping is the harshest noise, followed by depolarising, and then, phase damping.  All three negatively impact the QBER and, therefore, the SKR and the applicability of MDI-QKD in practical applications.

Repetition code was able to significantly reduce its impact, especially on amplitude damping; however, it's limited in high-noise applications and by resource constraints, as it requires a 3x increase in the amount of data sent.

The Hamming code is oversimplified for a quantum application (see future work), and the Steane code should be used instead.

Steane code is a much better implementation; however, it is hardware-limited, and that could lead to Eve masking. (see future work)

Eavesdropping can impact the QBER and SKR, however, not as much as any noise type, and so is much harder to correct for and also detect.

## Future Work

Whilst we were successful in reducing the impact of noise on MDI-QKD, there are certain areas which need development

For example:

A particularly interesting possibility involves hybrid quantum-classical correction systems. This would mean that an input of quantum data to a classical algorithm would be possible. There has been very little work done in this field - it remains mostly untapped due to the associated complications. After stumbling onto it, we have discussed using machine learning or a series of converter algorithms to achieve this, but due to a lack of time, implementing it is a major area of interest. This would hypothetically allow classical infrastructure to be used for quantum communication, which is why it is an area of such high interest, despite the numerous problems associated with its implementation. 

Eve masking is a particularly worrying side effect of our error correction code, as it would mean that anyone could theoretically listen in to any quantum communication. This should be addressed as soon as possible, likely through the creation of a more effective error correction algorithm, or perhaps development to MDI-QKD, where a 4th person could be involved. However, implementing this would require significant work. Machine learning could also be used here; however, the data set we currently have is very small, so that would be a challenge.

Whilst our Steane code works to correct both phase and bit flip errors, we only had time to implement a bit flip version of  repetition code. Perhaps this could be looked into and then developed into other error correction codes as it may work better for long-distance quantum communication, if used alongside Steane code. 


It's important to note that whilst Steane code gave better results, it was not fully noise tolerant, in order to achieve that, continuously variable error correction would have to be implemented, which is an area of high interest due to its theoretical perfection correction, which would also lead to MDI-QKD being highly accurate



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

