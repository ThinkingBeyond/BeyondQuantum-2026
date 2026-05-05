![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# QAOA vs. Classical Heurlistic

## Project Description

## Research Question

How does the solution quality of the standard Quantum Approximate Optimization Algorithm (QAOA) and Sahni-Gonzalez Algorithm compare in MaxCut instances on small, 3-, 4-, and 5-regular graphs?

We tested unweighted graphs with 10, 16, and 20 nodes, with instances of 3-, 4-, and 5-regular graphs, in order to assess how the performance of QAOA scaled as the number of edges per node increases.

## Motivation

Optimization problems are commonplace in real-life, with broad applications in areas such as marketing, finance, and engineering. Many of these optimization problems can be formatted as a Max-Cut problem. Finding an exact solution to these max-cut problems becomes exponentially more difficult as the complexity of the graphs increase however, meaning that only approximate solutions can be found for graphs above a certain complexity. QAOA offers a potential alternative to the classical apporiximation algorithms and could have the potential to surpass the effectiveness of classical approximation ratios if QAOA is able to effectively scale to the complexity of modern day application of the Max-Cut problem.

## Methods

We randomly generated graphs with 10, 16, and 20 nodes, with each number of nodes having 3 instances with 3, 4, and 5 connections on each node (example graph shown below). To measure the solution quality of the QAOA and SG algorithm we implemented a brute force algorithm that found the optimal cut of each graph, comparing it to the output of both the QAOA and the SG algorithm. Additionally we measured the number of two-qubit gates in each circuit that was created and average them across the 30 tests we ran of each graph to get an accurate idea of the average number of circuits needed to run the QAOA.

![Max-Cut Graph](Graph.png)

## Results
We found that the QAOA consistently found equivalent or slightly better quality solutions than the SG algorithm, with the level of solution quality staying relatively consistent from 0.97-0.99 for all the graphs. And the SG algorithm ranging from 0.98-0.96. The solution quality appears to decrease linearly over the 20 node graphs, but we are unsure if this is a real decrease in the solution quality or just the solution quality range appearing to decrease. More testing on higher node graphs would be required to confirm this.

![Approximation Ratio Comparison](Solution_Quality.png)

Additionaly we found that the number of two-qubit gates required to run the QAOA circuit increases in a roughly linear pattern, with the number of gates increasing alongside the number of connections as well. The number of two-qubit gates required more than doubled when going from 3-5 connections per node, indicating poor connection-wise scalability.

![Two-Qubit gates](Two-Qubit-Gates.png)

## Implications and Conclusion
While the QAOA appears to have a slight advantage in solution quality, it is severly hampered in the issue of scalabilty. The largest factor is the number of qubits required, since every additional node requires another qubit in the circuit. Current quantum technology has around 120-150 qubits avaliable, which limits the possible uses of QAOA to smaller scale instances. Additionally the number of two qubit gates that can be supported is around 5000, which again limits the use case to instances with less connections, since the number of two qubit gates required increases as more connections are added. For now classical algortihms remain the best option for real world applications, but with the advancement of quantum technology QAOA could be a competitive option for binary optimization problems.


[ ... ]

## Future Work

Graphs with node counts higher than 20 could be tested with the use of quantum hardware. Additionally there are different versions of QAOA that can be explored such as QAOA in QAOA and warm started QAOA. These versions appear to try to improve some of the scalability issues with QAOA.

## References


1. Zeqiao Z, Yuxuan D, Xinmei T, Dacheng T, QAOA-in-QAOA: solving large-scale MaxCut problems on small quantum machines (2022),  [arxiv](https://arxiv.org/abs/2205.11762)
2. Daniel P, Variational Quantum Algorithms for Combinatorial Optimization (2024), [arxiv](https://doi.org/10.48550/arXiv.2407.06421)
3. Ishan P, Akhil A, Hybrid Quantum-HPC Solutions for Max-Cut: Bridging Classical and Quantum Algorithms (2024), [arxiv](https://doi.org/10.48550/arXiv.2410.15626)
4. J. A. M, Kristel M, Toward a linear-ramp QAOA protocol: evidence of a scaling advantage in solving some combinatorial optimization problems (2025), npj quantum information, [nature](https://www.nature.com/articles/s41534-025-01082-1)
5. David B et al, Towards Robust Benchmarking of Quantum Optimization Algorithms (2025), [IEEE](10.1109/QCE60285.2024.11030870)
6. Micheal X, David W, Improved approximation algorithms for maximum cut and satisfiability problems using semidefinite programming (1995), [JACM](https://doi.org/10.1145/227683.227684)
7. IBM quantum platform, Quantum approximate optimization algorithm (2024), [IBM](https://quantum.cloud.ibm.com/docs/en/tutorials/quantum-approximate-optimization-algorithm)


---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

