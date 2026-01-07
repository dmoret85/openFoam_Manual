# Chapter 8 — Numerics and Stability

## 8.1 Numerical Stability as an Engineering Requirement

Numerical stability is not a secondary concern or a solver-specific technicality. It is a prerequisite for producing physically meaningful CFD results. A simulation that is numerically unstable may diverge immediately, oscillate indefinitely, or converge smoothly to an incorrect solution.

In OpenFOAM, numerical stability depends on the interaction between time integration, spatial discretization, solver settings, and mesh quality. Stability cannot be enforced by a single parameter; it must be designed into the case.

---

## 8.2 Time Integration and Time-Step Selection

Most engineering simulations in OpenFOAM are transient, even when a statistically steady solution is desired. The time step controls how information propagates through the domain and strongly influences stability.

A key non-dimensional parameter is the Courant–Friedrichs–Lewy (CFL) number:

\[
\mathrm{Co} = \frac{u \Delta t}{\Delta x}
\]

where \(u\) is the local velocity magnitude, \(\Delta t\) the time step, and \(\Delta x\) the local cell size.

General guidance:
- Explicit or semi-explicit schemes: \(\mathrm{Co} \lesssim 1\)
- VOF simulations: \(\mathrm{Co} \lesssim 0.5\)
- Highly transient flows: \(\mathrm{Co} \ll 1\)

Automatic time-step control using `adjustTimeStep` is strongly recommended for transient cases.

---

## 8.3 Spatial Discretization and `fvSchemes`

Spatial discretization choices directly affect numerical diffusion, boundedness, and stability.

Key principles:
- First-order schemes are stable but overly diffusive
- Higher-order schemes reduce diffusion but require better mesh quality
- Bounded schemes are essential for transported scalars and volume fractions

Typical engineering practice is to begin with conservative, bounded schemes and increase accuracy only after stability is demonstrated.

---

## 8.4 Pressure–Velocity Coupling

OpenFOAM’s segregated solvers rely on pressure–velocity coupling algorithms such as SIMPLE, PISO, and PIMPLE.

Key considerations:
- SIMPLE is suited for steady-state problems
- PISO is efficient for transient flows with small time steps
- PIMPLE blends SIMPLE and PISO and is robust for general transient simulations

Under-relaxation and corrector settings must be chosen consistently with time step and mesh resolution.

---

## 8.5 Linear Solvers and Tolerances

Linear solver settings influence convergence behavior but do not fix fundamental modeling or discretization errors.

Important points:
- Tight tolerances do not guarantee physical correctness
- Excessively loose tolerances mask instability
- Solver choice should reflect matrix symmetry and conditioning

Residuals should be interpreted as numerical indicators, not physical error measures.

---

## 8.6 Residuals, Convergence, and Physical Monitoring

Residual convergence alone is insufficient to assess solution quality.

Good practice includes monitoring:
- Integral quantities (forces, mass flow rates)
- Local probes and profiles
- Time histories of key variables

A solution is acceptable only when numerical convergence aligns with physical consistency.

---

## 8.7 Common Numerical Failure Modes

Typical numerical failure modes include:
- Time-step–induced divergence
- Pressure oscillations due to poor coupling
- Unbounded scalars or volume fractions
- False convergence caused by excessive relaxation

These issues often manifest before solver failure and should be treated as early warning signs.

---

## 8.8 Stabilization Strategies

Effective stabilization strategies include:
- Reducing time step or CFL limit
- Increasing numerical diffusion selectively
- Improving mesh quality in critical regions
- Adjusting pressure–velocity coupling parameters

Stabilization should be applied methodically, with physical implications considered at each step.

---

## 8.9 Engineering Checklist

Before trusting a solution:
- Verify CFL numbers throughout the domain
- Confirm boundedness of transported fields
- Check sensitivity to time step and discretization
- Ensure monitored physical quantities are stable

Numerical stability is not an obstacle to accuracy; it is the foundation upon which accuracy is built.
