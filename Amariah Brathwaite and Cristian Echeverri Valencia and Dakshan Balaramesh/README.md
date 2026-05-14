![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Qubit Manipulation in Quantum Circuits - Implementing Deutsch and Deutsch-Jozsa Algorithm for 2- and 3- and 4-Qubit Systems
The following project is done by Amariah Brathwaite, Cristian Echeverri Valencia and Dakshan Balaramesh, and mentored by Mr. Axel Karger. This project explores Qubit Manipulation, specifically using the Deutsch and Deutsch-Jozsa Algorithms.
## Overview

Quantum Computing is an innovative methodology that has transformed classical computational methods, as we know then today. Central to quantum computing is the qubit (quantum bit), which is an abstract mathematical object that can exist in a superposition of the classical bits (0 & 1). This prperty of qubits is often combined with entanglement, a phenomenon which posits that the state of one qubit is linked to another. When these two properties are combined with a thrird, quantum interference, quantum systems are then able to access and process information in a way that is much more powerful than classical computational methods.

Moreover, quantum computing employs quantum gates to manipulate qubits. These gates perform reversible, unitary operations that can be represented by matrices over complex Hilbert spaces. 

Quantum Computing employs several algorithms, two of which are the Deutsch and Deutsch-Josza Algorithms

There are only four possible functions of the form $$f: \{0,1\}\rightarrow \{0,1\}$$, which are the following:

| $$x$$  | $$f_1$$ | $$f_2$$ | $$f_3$$ | $$f_4$$ |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| 0 | 0 | 0 | 1 | 1 |
| 1  | 0 | 1 | 0 | 1 |

Classically, we may need two queries to guess if the function is either: 
* **Constant:** All outputs are the same.
* **Balanced:** Half outputs are 0s and half outputs are 1s.

However, Deutsch Algorithm made a conceptual proof that with a single query and a quantum computer we could get the most important characteristic of this function. This project explores the implementation of this algorithm and its natural succesor on the question of: How could we guess a function of the form $$f: \{0,1\}^n \rightarrow \{0,1\}$$


## Research Question

How can we implement the Deutsch Algorithm to functions $$f: \{0,1\} \rightarrow \{0,1\}$$ and the Deutsch-Jozsa Algorithm to functions  $$f: \{0,1\}^2 \rightarrow \{0,1\}$$ and $$f: \{0,1\}^3 \rightarrow \{0,1\}$$ to accurately predict if a function is constant or balanced?

## Motivation

At their inception, the Deutsch and Deutsch-Jozsa algortithms were supoosed to provide proof that quantum computers are more efficient than classical computers. These algorithms were not originally designed for real-world application, however there has been increased speculation regarding the capabilities of quantum computing.
Our main aim at this project is to evidence whether Deutsch and Deutsch-Jozsa Algorithms are an accurate approach to solve the main characteristic of $$f: \{0,1\}^n \rightarrow \{0,1\}$$-like functions contemporarily. 

## Method and Implemetation
This project heavily relies on oracles. These are functions that are embedded into a quantum circuit that perform the transformation $$|x\rangle |y\rangle \rightarrow |x\rangle |y\rangle &oplus; f(x)\rangle$$

For this project we implemented oracles for both constant functions (all inputs have the same output) and balanced functions (half the inputs result in 0 and the other half result 1)

To implement these oracle, these steps were taken:
1. Qubits were initialized to $$|1\rangle$$
   - Deutsch Algortithm: a single qubit
   - Deutsch-Josza Algortithm: $$n$$ qubits eg: 2, 3, 4
2. The qubits are then set in a superposition of states using a Hadamard gate
3.  The specific oracle gate was then composed into the circuit  
4.  The ibm_marrakesh backend was then used to capture data from a real quantum device
5.  The AerSimuator was used to provide theoretical results, for comparison.

## Results
Is is deduced that both algorithms can identify whether a function is constant or balanced in a single query. 
For the Deutsch Algorithm, it correctly identified Balanced functions by outputting $$|1\rangle$$ on the given input qubit.
Also, it was found that the balanced function predictions were less accurate than the constant function predictions for the algorithm.

<img width="1462" height="1229" alt="IMG_6381" src="https://github.com/user-attachments/assets/10594618-630e-4c4a-9b65-f057deb9a5dd" />

<img width="1609" height="1223" alt="IMG_6382" src="https://github.com/user-attachments/assets/1162711d-6a28-4f42-8548-eb5d186bd4f7" />

<img width="1969" height="1257" alt="IMG_6383" src="https://github.com/user-attachments/assets/aa1c93ab-aedb-4c29-b356-2b11c5078862" />


For the Deutshc-Jozsa Algorithm, it too identified the Balanced and Constant functions correctly with over 90% accuracy in both cases. 
And as in the Deutsch Algorithm, the prediction accuracy for Balanced functions was lower than for Constant functions.

<img width="1612" height="1331" alt="IMG_6384" src="https://github.com/user-attachments/assets/5829e785-49ae-413d-bce5-89f41168395c" />

<img width="1942" height="1348" alt="IMG_6386" src="https://github.com/user-attachments/assets/a98a3c77-f66f-48cd-afc0-74698d4a2a38" />

<img width="1939" height="1159" alt="IMG_6387" src="https://github.com/user-attachments/assets/0329d701-1869-46f2-9b72-6553a7ac2697" />




## Future Work

Using the same methods as the research, Deutsch-Jozsa Algorithm could be tested to 5-, 6- and 7- Qubit Systems to test whether the accuracies of prediction have a tendency depending on the functions. Future Research could be built upon instituting Error Correction into the "unknown" oracle, so in this way we could have a perfect oracle with an imperfect algorithm and then just test the effectiveness of Deutsch and Deutsch-Jozsa Algorithm by itself.

## References

- Weathers, Jeremy M. (2010). *Methods for quantum circuit design and simulation*. *Calhoun: The NPS Institutional Archive DSpace Repository*.

- Cleve, Richard, Ekert, Artur, Macchiavello, Chiara, & Mosca, Michele (1998). *Quantum Algorithms Revisited*. *Proceedings of The Royal Society A: Mathematical, Physical and Engineering Sciences*. https://doi.org/10.1098/rspa.1998.0164

- Jaradat, Yousef, Alia, Mohammad, Masoud, M., Mansrah, Ahmad, Jannoud, Ismael, & Alheyasat, Omar (2023). *Roadmap for Simulating Quantum Circuits Utilising IBM’s Qiskit Library: Programming Approach*. *The Eurasia Proceedings of Science, Technology, Engineering & Mathematics*. https://doi.org/10.55549/epstem.1412445

- Deutsch, D. (1985). *Quantum theory, the Church–Turing principle and the universal quantum computer*. *Proceedings of the Royal Society of London. A. Mathematical and Physical Sciences*. https://doi.org/10.1098/rspa.1985.0070

- Deutsch, D., & Jozsa, R. (1992). *Rapid solution of problems by quantum computation*. *Proceedings of the Royal Society of London. Series A: Mathematical and Physical Sciences*. https://doi.org/10.1098/rspa.1992.0167

- Kothari, K., & Chaudhuri, P. R. (2025). *Qubit Manipulation in Quantum Circuits - Solving Grover's Algorithm for 2- and 3-Qubit Systems*. *Beyond Quantum Proceedings 2025*.

- Youvan, Douglas (2023). *Quantum Oracles: Design, Implementation, and Implications in Quantum Search Algorithms*. https://doi.org/10.13140/RG.2.2.27075.78884

- Nakahara, Mikio, & Ohmi, Tetsuo (2008). *Quantum Computing - From Linear Algebra to Physical Realizations*. https://doi.org/10.1201/9781420012293

- Nielsen, Michael A., & Chuang, Isaac L. (2010). *Quantum Computation and Quantum Information: 10th Anniversary Edition*. Cambridge University Press.

- Qiskit Textbook. *Learn Quantum Computation using Qiskit*. https://qiskit.org/learn

- Javadi-Abhari, Ali, Treinish, Matthew, Krsulich, Kevin, Wood, Christopher J., Lishman, Jake, Gacon, Julien, Martiel, Simon, Nation, Paul D., Bishop, Lev S., Cross, Andrew W., Johnson, Blake R., & Gambetta, Jay M. (2024). *Quantum computing with Qiskit*. arXiv:2405.08810. https://arxiv.org/abs/2405.08810

- *Noise Analysis of Grover's Quantum Search Algorithm* (2023). *Indian Journal of Pure & Applied Physics*. https://doi.org/10.56042/ijpap.v61i5.69090
---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

