![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# How does the implementation of *n* logical constraints affect the search space and runtime of Grover’s Algorithm, investigated in the context of simplified molecular library search?

## Research Question

**The central inquiry of this study is:** *"How does the implementation of n logical constraints affect the search space and runtime of Grover’s Algorithm, investigated in the context of a simplified molecular library search?"*

**Core Objectives:**
Grover’s Algorithm provides a theoretical quadratic speedup for unstructured search problems where classical alternatives are limited. Our research explores the practical boundary of this speedup by *focusing on primary factors:*
- **Constraint Complexity (*n*):** We investigate how increasing the number of logical filters — such as toxicity, nitrogen presence, molecular size, and the presence of a ring — impacts the construction of the quantum Oracle.
- **Success Probability vs. Efficiency:** While additional constraints narrow the search space, they simultaneously increase circuit depth. We aim to identify the threshold where these constraints transition from being helpful filters to becoming a source of "noise" or complication that degrades the probability of a successful search.
- **Technical Context:** To address this question, we utilized a 4-qubit circuit in Qiskit to navigate a dataset of 16 molecules. Each molecule is mapped to a unique 4-bit code based on specific biochemical properties. This setup allows us to precisely monitor the phenomenon of over-rotation — a state where applying too many Grover iterations (*k*) causes the quantum state vector to rotate past the target solution, effectively "losing" the signal of the correct molecule.
- **Theoretical Significance:** By finding the precise balance of iterations (*k*) required for varying logical constraints, this research demonstrates how quantum searching can be optimized for identifying viable drug candidates in simplified chemical scenarios. Our findings highlight that maintaining accuracy in a quantum search is not just about having more constraints, but about managing the quantum state to avoid signal degradation.

## Motivation

In pharmaceutical research, virtual screening is an "unstructured search" problem — checking millions of potential drug candidates one by one. We chose this research question to test the efficiency of Grover's Algorithm, which theoretically offers a quadratic speedup over classical methods. By mapping molecular properties to logical constraints, we aim to identify the optimal threshold where quantum searching maintains high success probability before circuit complexity or over-rotation degrades the results.
As we are doing this research in a simplified form, we aimed to identify the effect adding constraints has on Grover, both due to expanding the search space, but also due to reducing the number of potential target solutions.
## Code and Implementations

The implementation is written in Python using the Qiskit framework. All required packages (such as qiskit, matplotlib, and numpy) are pre-installed within the environment scripts provided in the notebooks.

## Repository Structure
WRITE LATER

## Results
WRITE LATER

## Future Work

- **Scalability Testing:** Investigating how the optimal iteration count ($k$) and over-rotation threshold scale on 8-qubit or 10-qubit systems as the molecular library grows.
- **Hardware Implementation:** Testing these circuits on NISQ devices to analyze how physical gate errors and decoherence impact the success probability of complex Oracles.
- **Hybrid Workflows:** Integrating Grover’s search with the Variational Quantum Eigensolver (VQE) to first identify a candidate and then simulate its specific binding affinity or ground state energy.
- **Weighted Oracles:** Developing Oracles that prioritize specific chemical properties (e.g., toxicity vs. nitrogen presence) rather than treating all logical constraints as equal boolean filters.

## References
1. Bae, E., Shin, J., & Choi, M. (2026). Reducing circuit resources in Grover's algorithm via constraint-aware initialization. arXiv. https://doi.org/10.48550/arXiv.2601.17725

2. Grover, L. K. (1996). A fast quantum mechanical algorithm for database search. Proceedings of the 28th Annual ACM Symposium on Theory of Computing, 212–219. https://doi.org/10.1145/237814.237866

3. Guo, C. (2023). Grover’s algorithm – implementations and implications. Highlights in Science, Engineering and Technology, 38, 1071–1078. https://doi.org/10.54097/hset.v38i.5997

4. Hill, D. R. C. (2026). Grover quantum algorithm: Applications and limits. Encyclopedia, 6(4), 89. https://doi.org/10.3390/encyclopedia6040089

5. Jura, A. M. C., Jura, Ș. A., Popescu, D. E., Belengeanu, V., Gușiță, B., Pienar, C., Manea, A. M., & Boia, E. R. (2025). Quantum leap: Reshaping genetic diagnostics using quantum computing. Preprints. https://doi.org/10.20944/preprints202502.1371.v1

6. Lavor, C., Liberti, L., & Maculan, N. (2016). Grover’s algorithm applied to the molecular distance geometry problem. Proceedings of the Brazilian Conference on Neural Networks (CBRN), 1–4. https://doi.org/10.21528/CBRN2005-234

7. Olumide-Attah, A., Bagdasarian, R., & Ikenye, F. (2025). Quantum methods for modular exponentiation in Shor’s Algorithm.

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

