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

## Code and Implementations

The implementation is written in Python using the Qiskit framework. All required packages (such as qiskit, matplotlib, and numpy) are pre-installed within the environment scripts provided in the notebooks.

## Repository Structure
.
├── grover-molecular-search/
│   ├── grover_algorithm.ipynb               # Main research notebook (Implementation & Analysis)
│   ├── molecular_metadata.txt               # Mapping of molecules to bitstrings
│   └── statevector_results.txt              # Exported results of the quantum state
├── comparative-analysis/
│   ├── classical_vs_quantum.ipynb           # Benchmarking classical search vs Grover
│   └── complexity_graph.png                 # Visualization of search scaling
├── dataset/
│   └── molecular_library.csv                # The 16-molecule dataset with chemical properties
└── README.md                                # Project overview and research abstract

## Future Work

State and explain what follow-up research could be conducted based on your work.

## References

List all your references here. Remember to put links into markdown. For example:

1.  Einstein, A. (1905). *On the Electrodynamics of Moving Bodies*. Annalen der Physik, 17, 891-921. [Internet Archive](https://archive.org/details/einstein-1905-relativity)


---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

