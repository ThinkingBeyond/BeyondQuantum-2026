![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Quantum-Enhanced Spectral Analysis of Protein Energy Landscapes


## Research Question

Can a Non-Uniform Quantum Fourier Transform be used to identify protein active sites from non-uniform energy data and guide high-precision adaptive spline modeling?

## Motivation

Proteins change shape over time, and these changes are governed by complex energy landscapes. Molecular simulations generate huge amounts of data, but only a small part of it contains the most important information, such as transition regions. In addition, this data is often not evenly spaced, which makes it difficult to analyze using classical methods like standard Fourier analysis that rely on uniform sampling. This creates a need for methods that can handle irregular data efficiently.

To address this, we aim to combine data reduction techniques with a Non-Uniform Quantum Fourier Transform (NUQFT) to focus on the most relevant regions and analyze them effectively despite the non-uniform nature of the data.

## Implementation and Methods

We designed a pipeline that focuses only on the most important parts of the data.
First, we use a gradient-based approach to detect regions where the energy changes rapidly, since these are usually the most meaningful. These selected points are then grouped into clusters to separate different meaningful regions along the structure.

Next, we apply a quantum-inspired frequency analysis step. Instead of performing a full Non-Uniform Quantum Fourier Transform (NUQFT), which would compute all frequency components simultaneously, we estimate individual frequency components one at a time. This is done using the Hadamard test, where phase information is encoded into a quantum circuit and extracted through interference measured on an auxiliary qubit.

In this process, each circuit evaluates how strongly a specific frequency is present in the signal. By repeating this for multiple frequencies, we build a spectrum similar to a Fourier transform, even though the data is not uniformly sampled.

Because we evaluate frequencies sequentially and use a simulator rather than quantum hardware, the method does not achieve full quantum parallelism. Instead, it provides a quantum-inspired way of estimating spectral information from non-uniform data.

Finally, we reconstruct a smooth version of the energy landscape using interpolation, which helps visualize patterns and identify important regions such as potential active sites.

## Results

The pipeline reduces the dataset while preserving key transition regions identified through gradient-based sampling, as shown in the energy profile and structure plots. Clustering reveals that these important points are concentrated in specific regions rather than uniformly distributed.

The NUQFT step, implemented using the Hadamard test, produces a frequency spectrum with clear peaks, showing that meaningful patterns can be extracted from non-uniform data by estimating frequencies one at a time through quantum interference. The knot injection graph shows increased resolution in high-variation regions, and the spline reconstruction produces a smooth energy landscape that closely follows the original signal. The final graph highlights multiple candidate active sites, visible as local minima aligned with previously detected high-gradient regions.

<img width="600" height="596" alt="download (3)" src="https://github.com/user-attachments/assets/799aad00-d776-4d11-a0cb-ad8d17b37f8f" />


However, the method has limitations. The frequency analysis is performed sequentially rather than in full quantum parallelism, so it does not achieve true quantum speedup. Additionally, the results depend on parameter choices such as gradient thresholds and clustering gaps, which may affect stability. Finally, the approach is demonstrated on synthetic data, and performance on real molecular datasets remains to be validated.

## Future Work

Currently, the method is demonstrated on synthetic data generated within the code. In future work, we aim to extend the pipeline to real molecular dynamics datasets by introducing a data loading mechanism that can efficiently map external data into the model. In a quantum setting, this could involve designing a suitable data-loading operator or oracle to encode energy values directly into quantum states.

Further improvements include implementing the method on actual quantum hardware, optimizing parameter selection for more stable results, and extending the frequency analysis to capture additional information beyond the current approach. The pipeline could also be integrated with biological datasets to improve the identification of real protein active sites.

## References

1. Aftab, J., Khoo, Y., & Yang, H. (2026). Non-uniform quantum Fourier transform. arXiv.
2. Nielsen, M. A., & Chuang, I. L. (2010). Quantum computation and quantum information (10th anniversary ed.). Cambridge University Press.
3. Greengard, L., & Lee, J.-Y. (2009). Accelerating the nonuniform fast Fourier transform. SIAM Review, 51(3), 443–454. https://arxiv.org/abs/0811.3171
4. Robert, A., Barkoutsos, P. K., Woerner, S., & Tavernelli, I. (2021). Resource-efficient quantum algorithm for protein folding. npj Quantum Information, 7, 38. https://doi.org/10.1038/s41534-021-00368-4

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

