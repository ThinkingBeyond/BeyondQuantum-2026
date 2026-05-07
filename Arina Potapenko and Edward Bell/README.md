![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# How does the implementation of *n* logical constraints affect the search space and runtime of Grover’s Algorithm, investigated in the context of simplified molecular library search?

## Research Question

**The central inquiry of this study is:** *"How does the implementation of n logical constraints affect the search space and runtime of Grover’s Algorithm, investigated in the context of a simplified molecular library search?"*

**Core Objectives:**
Grover’s Algorithm offers a theoretical quadratic speedup for unstructured search problems. This study examines the practical limits of that speedup by focusing on:
- **Constraint Complexity *(n)*:** Investigating how increasing logical filters (e.g., toxicity, nitrogen presence, molecular size, ring structure) affects oracle construction and circuit complexity.
- **Success Probability vs. Efficiency:** While constraints refine the search, they also increase circuit depth and sensitivity to iteration count. We identify the point where additional constraints begin to reduce performance.
- **Technical Framework:** A 4-qubit Qiskit implementation was used to search a dataset of 16 molecules encoded as 4-bit strings, enabling controlled observation of algorithm behavior, including over-rotation.
- **Theoretical Insight:** Results show that optimal performance depends on balancing constraint strictness with the correct number of Grover iterations *(k)*, highlighting the importance of precise amplitude amplification.

## Motivation

In pharmaceutical research, virtual screening can be viewed as an unstructured search problem, where large numbers of candidate molecules must be evaluated. This study examines the efficiency of Grover’s Algorithm, which offers a theoretical quadratic speedup over classical methods. By mapping molecular properties to logical constraints, we investigate how increasing constraints affects performance, particularly in terms of solution density and sensitivity to over-rotation.
As we are doing this research in a simplified form, we aimed to identify the effect adding constraints has on the efficiency of Grovers algorithm, due to both the search space and the number of valid target solutions being affected. The implementation is written in Python using the Qiskit framework. All required packages (such as `qiskit`, `matplotlib`, and `numpy`) are pre-installed within the environment scripts provided in the notebooks.

## Results

**Overview:**
This study evaluates how the number of logical constraints *(n)* affects the performance of Grover’s Algorithm in a 4-qubit molecular search space *(N = 16)*. The analysis focuses on **three key aspects:**

- Probability amplification across iterations *(k)*
- Effect of solution density *(M)*
- Comparison with classical search scaling
  
**1. Iterative Probability Amplification**
- Grover’s Algorithm amplifies the probability of measuring target states through repeated application of the oracle and diffusion operator.
  
**For a single target state *(M = 1)*:**
- After *k = 1* iteration, the target state begins to show increased probability, but non-target states still retain significant amplitude.
- At *k = 3* iterations, the target state reaches maximum amplification, dominating the probability distribution.
- Beyond this point, additional iterations lead to over-rotation, reducing the probability of measuring the correct state.
  
**Key observation:**

- The algorithm exhibits oscillatory behavior, and optimal performance depends on selecting the correct number of iterations.


<img width="1243" height="475" alt="image" src="https://github.com/user-attachments/assets/fe7a40d5-daba-46b4-b660-2036c539acfd" />
&nbsp;

**2. Effect of Solution Density (*M*)**
The number of valid solutions (M) significantly impacts algorithm efficiency.

**M = 1**
- Requires the highest number of iterations
- Peak probability achieved at higher *k*

**M = 2–3**
- Fewer iterations required
- High success probability reached more quickly
  
**M = 4**
- Probability stabilizes around ~50%
- Algorithm shows reduced sensitivity to iteration count

**Key observation:**
- As *M* increases, fewer iterations are required, but the maximum achievable probability becomes more distributed across multiple valid states.

**Table 1: Success rate vs iterations for M = 1, 2, 3, 4**

| Iterations    | *M=1* Success | *M=2* Success | *M=3* Success | *M=4* Success |
| ------------- | ------------- |---------------|---------------|---------------|
| 0             | 0.125         | 0.25          | 0.375         | 0.5           |  
| 1             | 0.78125       | 1 (Opt)       | 0.84375       | 0.5           |
| 2             | 0.945312      | 0.25          | 0.023437      | 0.5           |
| 3             | 0.330078      | 0.25          | 0.990234 (Opt)| 0.5           |
| 4             | 0.012207      | 1             | 0.118652      | 0.5           |
| 5             | 0.547974      | 0.25          | 0.677124      | 0.5           |
| 6             | 0.999786 (Opt)| 0.25          | 0.571381      | 0.5           |
| 7             | 0.576973      | 1             | 0.19796       | 0.5           |
| 8             | 0.019457      | 0.25          | 0.95719       | 0.5           |
| 9             | 0.302891      | 0.25          | 0.001958      | 0.5           |
| 10            | 0.931266      | 1             | 0.914383      | 0.5           |


<img width="600" height="470" alt="image" src="https://github.com/user-attachments/assets/e6c61681-6cb0-42bb-bed4-066ef95d8dc9" />

&nbsp;

**3. Optimal Iteration Counts**
**Table 2.** The experimentally observed optimal iteration values are:

| M (solutions)  | Best integer (k) | Plotted Average (k)| Max Success Rate|
| -------------  | -----------------|--------------------|-----------------|
| 1              | 6                | 6.016578           | 0.999786        |
| 2              | 1                | 1                  | 1               |
| 3              | 3                | 3.025896           | 0.990234        |      
| 4              | 0                | 0.5                | 0.5             |

**Key observation:**
 - Optimal k decreases as the number of valid solutions increases, consistent with theoretical predictions.

**4. Scaling Behavior vs Classical Search**
- Grover’s Algorithm was compared to classical linear search for *N = 16*
- The quantum implementation required fewer iterations to locate target states, consistent with the expected quadratic speedup.

**Key observation:**
- The advantage of Grover’s Algorithm becomes more pronounced as the size of the search space increases.

<img width="989" height="690" alt="image" src="https://github.com/user-attachments/assets/c74bf6b1-73cd-4ccf-8a98-d5b9a1b5df00" />


## Findings Summary:
- Increasing logical constraints reduces the number of valid solutions *(M)*
- Lower M requires more Grover iterations *(k)*
- The algorithm becomes more sensitive to iteration count as *M* decreases
- Over-rotation occurs when *k* exceeds the optimal value
- Observed behavior matches theoretical predictions of Grover’s Algorithm

## Future Work

- **Scalability Testing:** Investigating how the optimal iteration count *(k)* and over-rotation threshold scale on 8-qubit or 10-qubit systems as the molecular library grows.
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

