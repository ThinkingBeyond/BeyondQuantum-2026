![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Entanglement Entropy Scaling and MPS Simulability of Quantum Algorithms

This project explores the classical limits of quantum computation by studying the entanglement produced by well-known quantum algorithms. Normally, quantum computing focuses on circuit depth and speedup, but in this project we have used entanglement entropy as a key metric for whether a quantum algorithm is classically simulatable or not. By representing quantum states as Matrix Product States (MPS), we tried to draw a line between algorithms that remain classically simulatable and those which are not feasible to simulate classically.

## Research Question

How does entanglement entropy scale with the number of qubits in quantum algorithms, and how does this scaling affect the classical simulation cost? 
We have used 3 Algorithms:
1. Quantum Approximate Optimization Algorithm (QAOA)
2. Grover's Algorithm
3. 1D Discrete Time Quantum Walk

## Motivation

As quantum hardware enters the NISQ era, pinpointing the boundary of quantum advantage is more urgent than ever. Circuit depth alone is a poor measure of hardness — a deep circuit with low entanglement can still be efficiently simulated on a laptop. By using von Neumann entropy SvN and bond dimension χ as complexity proxies, we can define a practical "simulability boundary" that goes beyond theoretical complexity classes and speaks directly to what current hardware can or cannot do.

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


## Results

### 1. Grover’s Algorithm

- Entropy capped at **1 bit**  
- Bond dimension: **χ = 2 (constant)**  
- AIC favors **logarithmic scaling**

**Conclusion:**
- Obeys **Area Law**  
- Efficiently **MPS simulatable**


### 2. QAOA (MaxCut)

- Entropy grows **linearly** with qubits and depth  
- Bond dimension approaches **2^(n/2)**  
- AIC favors **linear scaling**

**Conclusion:**
- Obeys **Volume Law**  
- **Classically intractable**


### 3. Quantum Walks

- Show **finite-size saturation effects**  
- Exhibit **local Volume-Law-like behavior**

**Conclusion (partially empirical):**
- Hard at small scales  
- Large-scale behavior remains **unverified**

## Future Work

State and explain what follow-up research could be conducted based on your work.

## References

- M. A. Nielsen and I. L. Chuang, Quantum Computation and Quantum Information, Cambridge University Press, 2011
- S. M. Barnett, Introduction to Quantum Information, Oxford University Press, 2009
- X.-X. Fang et al., "Maximal Coin-Position Entanglement Generation in a Quantum Walk," Phys. Rev. A 107, 012433 (2023)


---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

