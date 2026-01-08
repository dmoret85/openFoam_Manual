# Chapter 12 — Debugging and Common Failure Modes

## 12.1 Debugging Philosophy

Most OpenFOAM simulations that fail do not fail catastrophically. They often run, converge numerically, and produce smooth fields that are nevertheless physically wrong. Debugging CFD therefore requires a different mindset than debugging software.

The goal of debugging is not to eliminate solver errors, but to identify **violations of physical, modeling, or numerical assumptions**. OpenFOAM is generally explicit when numerical limits are exceeded; more subtle errors must be detected by the user. Debugging CFD is therefore an exercise in validating assumptions, not tuning parameters until the solver stops complaining.

---

## 12.2 Categories of Failure

CFD failures typically fall into three overlapping categories:

- **Physical modeling failures**  
- **Mesh-related failures**  
- **Numerical stability failures**

Correct diagnosis requires isolating which category dominates before attempting corrective action.

These categories are not mutually exclusive. A numerical failure is often triggered by a mesh or modeling issue, even if it manifests as solver divergence.

---

## 12.3 Physical Modeling Failures

Physical modeling failures occur when the chosen equations or models are inconsistent with the real flow.

Common indicators:
- Unphysical velocity or pressure levels
- Incorrect mass or energy balances
- Sensitivity to arbitrary parameter changes

Typical causes include:
- Inappropriate turbulence model
- Inconsistent boundary conditions
- Invalid assumptions (e.g. incompressibility, steady flow)

These failures often persist even on refined meshes and stable numerics.

---

## 12.4 Mesh-Related Failures

Mesh-related failures arise when the spatial discretization cannot represent the required physics.

Symptoms include:
- Excessive numerical diffusion
- Spurious oscillations near boundaries
- Poor prediction of wall quantities

Common causes:
- Inadequate resolution of boundary layers or shear layers
- Excessive skewness or non-orthogonality
- Abrupt refinement transitions

Mesh problems often manifest as numerical instability but cannot be fixed through solver settings alone.

Mesh-related failures often appear only after numerics are made more accurate, as excessive numerical diffusion can initially mask mesh deficiencies.

---

## 12.5 Numerical Stability Failures

Numerical failures are caused by inconsistent time stepping, discretization, or solver control.

Typical symptoms:
- Rapid divergence or floating-point exceptions
- Residuals that oscillate or stagnate
- Unbounded scalars or volume fractions

Frequent causes:
- Excessive CFL number
- Incompatible discretization schemes
- Overly aggressive under-relaxation removal

Numerical stabilization should always be applied conservatively and reversibly.

---

## 12.6 False Convergence

False convergence occurs when residuals decrease but the solution is not physically correct.

Indicators:
- Stable residuals with drifting forces or fluxes
- Grid-sensitive “converged” results
- Non-physical flow features that persist

False convergence is common in steady-state RANS simulations and must be identified using physical monitoring, not residuals alone.

---

## 12.7 Debugging Strategy

A systematic debugging approach includes:

1. Verify physical assumptions and boundary conditions  
2. Check mesh quality and resolution in critical regions  
3. Reduce time step and simplify numerics  
4. Start with conservative turbulence and discretization models  
5. Monitor physically meaningful quantities  

These steps should be followed in order. Skipping directly to numerical tuning often obscures the true source of failure.
Changes should be applied incrementally and evaluated independently.

---

## 12.8 Tools for Diagnosis in OpenFOAM

Useful OpenFOAM tools include:
- `checkMesh` for geometric diagnostics  
- Field probes and sampling utilities  
- Residual and time-history monitoring  
- Visualization of gradients and fluxes  

Visualization is a diagnostic tool, not proof of correctness.

---

## 12.9 When to Stop Debugging

Debugging should stop when:
- Physical trends are consistent
- Results are insensitive to reasonable numerical changes
- Assumptions are explicitly acknowledged

Further refinement beyond this point may increase cost without improving engineering value.

---

## 12.10 Engineering Mindset

CFD debugging is not about achieving perfect convergence or eliminating all numerical artifacts. It is about establishing **confidence in the model within known limits**.

A simulation that is understood and bounded is more valuable than one that appears perfect but is poorly diagnosed.

## 12.11 Symptom-to-Cause Mapping

| Symptom | Likely dominant cause |
|------|----------------------|
| Immediate divergence | Time step too large, severe mesh defects |
| Oscillating residuals | Poor pressure–velocity coupling, outlet issues |
| Smooth but wrong solution | Physical modeling failure, false convergence |
| Unbounded turbulence variables | Skewness, aggressive schemes |
| Sensitivity to relaxation factors | Mesh or BC inconsistency |

This table should be used as a starting point for diagnosis, not as a substitute for systematic analysis.

