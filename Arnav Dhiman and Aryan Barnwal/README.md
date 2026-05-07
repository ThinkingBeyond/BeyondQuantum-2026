![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# ENTANGLEMENT ENTROPY SCALING AND MPS SIMULABILITY OF QUANTUM ALGORITHMS

## Research Question
Our primary research question investigates when a quantum algorithm actually requires a quantum computer to be simulated. Specifically, we ask whether three canonical quantum algorithms Grover's search, the Quantum Approximate Optimization Algorithm (QAOA), and the discrete time coined Quantum Walk (QW) generate entanglement structures that remain within the reach of classical Matrix Product State (MPS) simulation. We test the criterion that an algorithm is MPS simulatable if and only if its entanglement entropy remains sub linear in system size throughout its execution.

## Motivation
The circuit model alone is insufficient for answering the question of quantum advantage, as a deep circuit acting on a low entanglement state can still be efficiently simulated on a classical machine. The true bottleneck for classical simulation is entanglement. 

Matrix Product States (MPS) serve as the leading classical ansatz for one dimensional quantum systems. If the entanglement entropy of a state's bipartition follows an area law scaling as SvN = O(log n) the bond dimension chi grows only polynomially, making MPS simulation tractable. Conversely, if it follows a volume law scaling as SvN = O(n) the bond dimension grows exponentially, rendering simulation classically hard. By empirically characterizing the entanglement laws obeyed by the output states of these algorithms, we can create a concrete map of where classical simulation breaks down.

## Methodology and Implementation
Our experimental setup involves analyzing the entanglement dynamics of Grover's Algorithm, QAOA, and the discrete time coined Quantum Walk across various system sizes and circuit depths. 

* Simulation and Measurement
* We extracted the statevectors for each algorithm via exact simulation using Qiskit.
* We computed the von Neumann entropy of the system by applying a partial trace to the statevector, performing Singular Value Decomposition (SVD), and calculating the entropy from the singular values.
* We calculated the effective bond dimension using truncated SVD with a threshold of epsilon = 10 to the power of negative 6.

* Classification Framework
To determine the simulability boundaries, we extracted the peak entropy as a function of system size. We then fit two competing models to this data:
1. Area Law Model: f log(n) = a log2 n + b
2. Volume Law Model: f lin(n) = c n + d

Classification was performed using the Akaike Information Criterion (AIC) to select the best fitting model. If the logarithmic model fit better, the algorithm was classified as TRACTABLE, and if the linear model fit better, it was classified as HARD.

## Results
Our empirical measurements successfully characterized the simulability boundary for each of the three algorithms, revealing fundamentally different entanglement structures.

* Grover's Search: Conclusively MPS tractable. The entropy exhibits regular, oscillatory behavior, peaking at exactly 1.0 bit regardless of system size, and requires a constant bond dimension of chi = 2 across all system sizes. The logarithmic model vastly outperformed the linear model, confirming an area law. AIC log = negative 34.3, AIC lin = negative 27.2.
* QAOA: Classically hard beyond shallow depths. The entropy rapidly and monotonically increases with circuit depth and qubit count, showing no signs of an area law cap. The linear model provided a superior fit, placing QAOA in the volume law regime. AIC log = negative 6.8, AIC lin = negative 7.6.
* Discrete Quantum Walk: Strongly hard. The coin position entanglement entropy grows proportionally with the width of the position register. This yielded the most decisive classification, with the linear model outperforming the logarithmic model by an extraordinarily large margin. AIC log = negative 256.9, AIC lin = negative 427.4.

## Conclusion
This study provides an empirically grounded map of classical simulability boundaries for structured versus variational quantum algorithms. 

We demonstrated that computational advantage does not inherently require highly entangled, volume law states. Grover's algorithm remains confined to a low entanglement manifold, meaning tensor network methods like MPS can simulate it efficiently despite its quadratic speedup. Conversely, QAOA acts as a quantum scrambler that heavily correlates distant qubits, driving a global entanglement spread that quickly hits a volume law bottleneck. Similarly, the discrete Quantum Walk rapidly spreads coin position entanglement to the full available capacity of its exponentially larger position space. 

Ultimately, entanglement entropy measurement should precede decisions regarding whether a quantum or classical backend is appropriate for a given algorithmic task, as exact statevector simulators are entirely blind to these underlying entanglement dynamics.

## Future Work
Future investigations should extend this analysis to native MPS simulation backends, such as TeNPy or ITensor, to directly validate the runtime savings predicted by our bond dimension analysis. Additionally, applying this framework to larger system sizes using direct quantum hardware will provide further insight into these entanglement boundaries.

## References
1. L. K. Grover, "A fast quantum mechanical algorithm for database search," in Proc. 28th Annual ACM Symposium on Theory of Computing (STOC), pp. 212 to 219, 1996.
2. E. Farhi, J. Goldstone, and S. Gutmann, "A quantum approximate optimization algorithm," arXiv 1411.4028, 2014.
3. G. Vidal, "Efficient classical simulation of slightly entangled quantum computations," Physical Review Letters, vol. 91, no. 14, p. 147902, 2003.
4. M. B. Hastings, "An area law for one dimensional quantum systems," Journal of Statistical Mechanics Theory and Experiment, vol. 2007, no. 08, p. P08024, 2007.
5. Y. Aharonov, L. Davidovich, and N. Zagury, "Quantum random walks," Physical Review A, vol. 48, no. 2, pp. 1687 to 1690, 1993.
6. J. Kempe, "Quantum random walks an introductory overview," Contemporary Physics, vol. 44, no. 4, pp. 307 to 327, 2003.
7. F. G. S. L. Brandão et al., "Models of quantum complexity growth," PRX Quantum, vol. 2, no. 3, p. 030316, 2021.
8. U. Schollwöck, "The density matrix renormalization group in the age of matrix product states," Annals of Physics, vol. 326, no. 1, pp. 96 to 192, 2011.
9. L. Zhou et al., "Quantum approximate optimization algorithm Performance, mechanism, and implementation on near term devices," Physical Review X, vol. 10, no. 2, p. 021067, 2020.
10. H. Akaike, "A new look at the statistical model identification," IEEE Transactions on Automatic Control, vol. 19, no. 6, pp. 716 to 723, 1974.

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

