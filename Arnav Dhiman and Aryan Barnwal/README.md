![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Entanglement Entropy Scaling and MPS Simulability of Quantum Algorithms

This project explores the classical limits of quantum computation by studying the entanglement produced by well-known quantum algorithms. Normally, quantum computing focuses on circuit depth and speedup, but in this project we have used entanglement entropy as a key metric for whether a quantum algorithm is classically simulatable or not. By representing quantum states as Matrix Product States (MPS), we tried to draw a line between algorithms that remain classically simulatable and those which are not feasible to simulate classically.

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

## Research Question

State your research question here and elaborate on it.
How does entanglement entropy scale with the number of qubits in quantum algorithms, and how does this scaling affect the classical simulation cost? 
We have used 3 Algorithms:
1. Quantum Approximate Optimization Algorithm (QAOA)
2. Grover's Algorithm
3. 1D Discrete Time Quantum Walk

## Motivation

Explain your motivation for your chosen research question here.

As quantum hardware enters the NISQ era, pinpointing the boundary of quantum advantage is more urgent than ever. Circuit depth alone is a poor measure of hardness — a deep circuit with low entanglement can still be efficiently simulated on a laptop. By using von Neumann entropy (SvNS_{vN}
SvN​) and bond dimension (χ\chi
χ) as complexity proxies, we can define a practical "simulability boundary" that goes beyond theoretical complexity classes and speaks directly to what current hardware can or cannot do.

## Methodology

**Classification Framework**
Algorithms are categorized by how their peak entropy S_vn(max) scales with system size n.
We use the Akaike Information Criterion (AIC) to determine which model best fits the empirical data:

Logarithmic scaling O(log⁡n) -> Area Law -> Classically Tractable
Linear scaling O(n) -> Volume Law -> Classically Hard

**Measurement Pipeline**

Statevector Extraction — Exact statevectors generated via Qiskit
SVD Analysis — Statevector reshaped across a balanced bipartition, then decomposed via Singular Value Decomposition
Entropy Calculation — Von Neumann entropy computed from the resulting Schmidt coefficients



Continue working through the points listed above with the help of sensibly named subsections. 

If you want to see some good examples of README files check out:
- [Example 1](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/warenya-loulia/README.md)
- [Example 2](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/shaana-karuna/README.md)

[ ... ]

## Results

Grover's Search is structurally confined to a two-dimensional subspace. Entropy is capped at exactly 1.0 bit, and bond dimension stays flat at χ=2 regardless of system size. Its quadratic speedup over classical brute force does not require, and does not generate, complex entanglement. It is efficiently simulatable by MPS.
QAOA (MaxCut): Entropy grows linearly with both circuit depth p and qubit count n, and bond dimension rapidly saturates the theoretical maximum of 2^(n/2)
2n/2. This is the hallmark of Volume Law behavior and genuine classical hardness.
Quantum Walks exhibit what we term finite-size hardness: boundary reflections of the wavefunction cause premature entropy saturation in small registers, producing locally Volume-Law-like behavior that may relax at larger system sizes.

## Future Work

State and explain what follow-up research could be conducted based on your work.

## References

M. A. Nielsen and I. L. Chuang, Quantum Computation and Quantum Information, Cambridge University Press, 2011
S. M. Barnett, Introduction to Quantum Information, Oxford University Press, 2009
X.-X. Fang et al., "Maximal Coin-Position Entanglement Generation in a Quantum Walk," Phys. Rev. A 107, 012433 (2023)

List all your references here. Remember to put links into markdown. For example:

1.  Einstein, A. (1905). *On the Electrodynamics of Moving Bodies*. Annalen der Physik, 17, 891-921. [Internet Archive](https://archive.org/details/einstein-1905-relativity)

**Tip**: *If you have you references in BibTex, Google Scholar or Zotero*
1. Create/copy a list into ChatGPT
2. Ask it to turn it into an unsorted list in markdown

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

