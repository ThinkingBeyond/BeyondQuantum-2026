![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Simulating Bohmian Trajectories

## Research Question

**How does entanglement - whether from bosonic symmetrisation or dynamically-induced phase coupling - alter the deterministic Bohmian trajectories, scattering statistics, and velocity correlations of a two-particle system scattering off a Gaussian barrier?**

In this research project, we will be comparing how trajectories of Bosonic Symmetric Entanglement and Phase-Induced Entanglement differ when they interact with a Guassian Potential barrier. We model the particles in each state as a Guassian wave packet, and we use numerical methods such as Crank-Nicolson, RK4 & RK45 - providing a comparison between each RK4 and RK45 - to simulate and evolve the trajectories. We also use metrics and measures such as Entorpy, Velocity correlation, Independence ratio, Initial and Final densities to validate our results.

## Motivation

Standard quantum mechanics predicts the results of measurements with great accuracy, but says nothing about what particles actually do between measurements. Bohmian mechanics solves this by giving particles definite positions at all times, guided by a pilot wave. $\Psi(x_1, x_2, t)$:

$$\dot{x}_k = \frac{\hbar}{m} \mathrm{Im}\!\left(\frac{\partial_{x_k}\Psi}{\Psi}\right)$$

In the case of entangled states the velocity of particle 1 depends instantaneously on the position of particle 2, and thus entanglement non-locality is directly visible in individual trajectories. This project asks if we can see that fingerprint in a controlled scattering simulation.

---
## Method

We compare three two-particle initial states scattering off a Gaussian barrier $V(x_1, x_2) = V_1(x_1) + V_1(x_2)$:

| Stage | State | Entanglement |
|-------|-------|-------------|
| **1** | Product state $\varphi_A(x_1) \otimes \varphi_B(x_2)$ | Independent baseline |
| **2A** | Symmetric (bosonic) $\mathcal{N}[\varphi_A\varphi_B + \varphi_B\varphi_A]$ | Built into initial state |
| **2B** | Product state + phase ramp $\Psi \cdot e^{i\alpha(t)(x_1-x_2)^2}$ | Induced during evolution |

Since stages 2A and 2B have the same initial marginal densities as stage 1 (confirmed by KL divergence), the only thing that changes is the entanglement.

**Numerical methods:** Crank-Nicolson for wave function evolution, RK4 for trajectory integration (checked against RK45 for a subsample), Born-rule $\chi^2$ test to check for quantum equilibrium at all times.

**Metrics tracked:**KL divergence, independence ratio 
$I = P(TT)/[P(T_1)\cdot P(T_2)]$, velocity correlation $\rho_v(t)$ entanglement entropy $S_e$, conservation of norm, and Born-rule $\chi^2$.



---
### Physical Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Domain | $x \in [-20, 20]$ | Simulation box with absorbing boundaries |
| Grid points | $256 \times 256 = 65{,}536$ DOF | Two-body configuration space |
| Time window | $t \in [0, 5]$, 600 steps | $\Delta t \approx 0.00833$ |
| Barrier height | $V_0 = 5.0$ | Partial transmission regime |
| Barrier width | $\sigma_b = 0.8$ | Gaussian half-width |
| Particle A momentum | $p_A = 3.2 \Rightarrow KE_A \approx 5.12$ | Near-barrier — mixed T/R |
| Particle B momentum | $p_B = 2.8 \Rightarrow KE_B \approx 3.92$ | Below barrier — reflection favoured |
| Wavepacket width | $\sigma = 2.0$ | Minimum-uncertainty Gaussian |
| Phase coupling | $\alpha_\text{max} = 0.6$, ramp $t_\text{ramp} = 1.5$ | Stage 2B only |
| Ensemble size | $N_\text{traj} = 300$ per stage | Born-rule sampled initial positions |

### Numerical Stack

| Component | Method | Justification |
|-----------|--------|---------------|
| Wave function propagation | **Crank-Nicolson** (implicit, sparse LU) | Unconditionally stable; exact norm conservation |
| Trajectory integration (primary) | **RK4** (fixed step) | 4th-order accuracy; efficient for large ensembles |
| Trajectory integration (validation) | **RK45** (adaptive via `scipy.solve_ivp`) | Cross-checks RK4 fidelity on 60-trajectory subsample |
| Born-rule verification | **$\chi^2$ test** at $t_\text{mid}$ | Confirms quantum equilibrium is maintained |

### Key Equations

| Equation | Formula |
|----------|---------|
| Guidance equation | $\dot{x}_k = \frac{\hbar}{m} \mathcal{Im}\!\left(\frac{\partial_{x_k}\Psi \cdot \Psi^*}{|\Psi|^2}\right)$ |
| Crank-Nicolson step | $(I + irH)\Psi^{n+1} = (I - irH)\Psi^n$ |
| Phase kernel (Stage 2B) | $\Psi \rightarrow \Psi \cdot \exp(i\,\Delta\alpha(t)(x_1-x_2)^2)$ |
| Bosonic symmetrisation | $\Psi = \mathcal{N}[\varphi_A(x_1)\varphi_B(x_2) + \varphi_B(x_1)\varphi_A(x_2)]$ |
| Von Neumann entropy | $S_e = -\sum_k \lambda_k \log \lambda_k$ |
| Independence ratio | $I = P(TT)\,/\,[P(T_1) \cdot P(T_2)]$ |
| Born-rule $\chi^2$ | $\chi^2_\text{red} = \frac{1}{\nu}\sum\frac{(O-E)^2}{E}$ |

### Validation & Metrics

Six quantitative measures are tracked across all stages:

1. **KL Divergence** — checks identical marginal densities at 𝑡 = 0 for all stages, confirming a fair start
2. **Independence Ratio** $I = P(TT)\,/\,[P(T_1)\cdot P(T_2)]$ - $I \neq 1$ is a clear signature that entanglement is shaping the outcome of scattering
3. **Norm Conservation** $\|\Psi^n\|\,/\,\|\Psi^0\|$ - Crank-Nicolson keeps it at machine precision all the tim
4. **Velocity Correlation** $\rho_v(t)$ (Pearson) - non-zero in entangled stages; trajectory-level fingerprint of Bohmian non-locality
5. **Born-rule $\chi^2$** - ensemble positions must follow $|\Psi|^2$ at $t_\text{mid}$ to confirm quantum equilibrium
6. **Entanglement Entropy** $S_e$ - computed by Schmidt decomposition (SVD) at sampled time steps

### Code Structure


---

## Results


### Initial State Verification (KL Divergences)

| Comparison | KL Divergence | Verdict |
|------------|--------------|---------|
| Stage 1 vs Stage 2A (marginals) | *(insert value)* | *(fair start ✓ / ⚠)* |
| Stage 1 vs Stage 2B (marginals) | *(insert value)* | *(fair start ✓ / ⚠)* |

### Scattering Outcome Fractions

| Stage | TT (%) | RR (%) | TR (%) | RT (%) | Independence Ratio $I$ |
|-------|--------|--------|--------|--------|----------------------|
| Stage 1 - Product | | | | | *(≈ 1.0 expected)* |
| Stage 2A - Symmetric | | | | | |
| Stage 2B - Phase-Induced | | | | | |

### Velocity Correlations $\rho_v(t)$

### Entanglement Entropy $S_e(t)$


### Final Position Densities

| Stage 1 (Product) | Stage 2A (Symmetric) | Stage 2B (Phase-Induced) |
|:-----------------:|:--------------------:|:------------------------:|
| ![](s1_final.png) | ![](s2a_final.png)   | ![](s2b_final.png)       |

### Bohmian Trajectory Braids (3D Configuration Space)

*Insert rotating 3D braid animations — one per stage — showing $(x_1, x_2, t)$ trajectory bundles colour-coded by scattering outcome (TT=green, RR=red, TR=yellow, RT=blue).*

---

## Conclusions

*(To be completed after results are obtained.)*

Preliminary expectations based on theory:

- **Stage 1** should show $I \approx 1$ and $\rho_v \approx 0$, confirming that product-state particles scatter independently with no velocity correlations.
- **Stage 2A** should show $I \neq 1$ and a non-zero $\rho_v(t)$ arising from the bosonic exchange symmetry encoded in the initial state.
- **Stage 2B** should show $\rho_v(t)$ growing from zero during the phase ramp ($t < t_\text{ramp} = 1.5$) and stabilising thereafter, directly visualising the *build-up* of dynamically induced entanglement in Bohmian trajectory space.

---

## Future Work



---

## References

**Foundational Bohmian Mechanics**

1. Bohm, D. (1952). A Suggested Interpretation of the Quantum Theory in Terms of "Hidden" Variables I & II. *Physical Review*, 85, 166–193. [doi:10.1103/PhysRev.85.166](https://doi.org/10.1103/PhysRev.85.166)



> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

