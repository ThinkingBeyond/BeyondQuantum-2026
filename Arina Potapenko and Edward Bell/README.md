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
As we are doing this research in a simplified form, we aimed to identify the effect adding constraints has on the efficiency of Grovers algorithm, due to both the search space and the number of valid target solutions being affected. The implementation is written in Python using the Qiskit framework. All required packages (such as qiskit, matplotlib, and numpy) are pre-installed within the environment scripts provided in the notebooks.

## Results

**Overview:**
This study evaluates how the number of logical constraints *(n)* affects the performance of Grover’s Algorithm in a 4-qubit molecular search space **(N = 16). The analysis focuses on **three key aspects:**

- Probability amplification across iterations *(k)*
- Effect of solution density *(M)*
- Comparison with classical search scaling
  
**1.Iterative Probability Amplification**
- Grover’s Algorithm amplifies the probability of measuring target states through repeated application of the oracle and diffusion operator.
  
**For a single target state *(M = 1)*:**
- After *k = 1* iteration, the target state begins to show increased probability, but non-target states still retain significant amplitude.
- At *k = 3* iterations, the target state reaches maximum amplification, dominating the probability distribution.
- Beyond this point, additional iterations lead to over-rotation, reducing the probability of measuring the correct state.
  
**Key observation:**

- The algorithm exhibits oscillatory behavior, and optimal performance depends on selecting the correct number of iterations.

<img width="1243" height="475" alt="image" src="https://github.com/user-attachments/assets/fe7a40d5-daba-46b4-b660-2036c539acfd" />


**2. Effect of Solution Density (*M*)**

The number of valid solutions (M) significantly impacts algorithm efficiency.

**M = 1**
- Requires the highest number of iterations
- Peak probability achieved at higher k
**M = 2–3**
- Fewer iterations required
- High success probability reached more quickly
**M = 4**
- Probability stabilizes around ~50%
- Algorithm shows reduced sensitivity to iteration count

**Key observation:**
- As *M* increases, fewer iterations are required, but the maximum achievable probability becomes more distributed across multiple valid states.

###**Success rate vs iterations for M = 1, 2, 3, 4**

| Iterations    | *M=1* Success | *M=2* Success | 
| ------------- | ------------- |---------------|
| 0             | 0.125         | 0.25          |
| 1             | 0.78125       | 1 (Opt)       |
| 2             | 0.945312      | 0.25          |
| 3             | 0.330078      | 0.25          |
| 4             | 0.012207      | 1             |
| 5             | 0.547974      | 0.25          |
| 6             | 0.999786 (Opt)| 0.25          |
| 7             | 0.576973      | 1             |
| 8             | 0.019457      | 0.25          |
| 9             | 0.302891      | 0.25          |
| 10            | 0.931266      | 1             |


<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/e6c61681-6cb0-42bb-bed4-066ef95d8dc9" />

**3. Optimal Iteration Counts**
The experimentally observed optimal iteration values are:

M (solutions)	Optimal k	Max Success Probability
1	6	~0.9998
2	1	~1.0
3	3	~0.99

Key observation:
Optimal k decreases as the number of valid solutions increases, consistent with theoretical predictions.

📌 Insert Table: Summary of optimal parameters

4. Scaling Behavior vs Classical Search

Grover’s Algorithm was compared to classical linear search for N = 16:

Classical search complexity:

O(N)

Quantum search complexity:

O(
N
	​

)

The quantum implementation required fewer iterations to locate target states, consistent with the expected quadratic speedup.

Key observation:
The advantage of Grover’s Algorithm becomes more pronounced as the size of the search space increases.

📌 Insert Graph: Classical vs quantum complexity scaling

5. Summary of Findings
Increasing logical constraints reduces the number of valid solutions (M)
Lower M requires more Grover iterations (k)
The algorithm becomes more sensitive to iteration count as M decreases
Over-rotation occurs when k exceeds the optimal value
Observed behavior matches theoretical predictions of Grover’s Algorithm

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

7. Ayman, Judy., Hakeem, Manal. (2024). Grover’s Algorithm. https://github.com/ThinkingBeyond/IQRG-2024 

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

