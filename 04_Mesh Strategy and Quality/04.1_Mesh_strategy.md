# Chapter 4 — Mesh Strategy and Quality

## 4.1 Role of the Mesh in CFD

In finite-volume CFD, the mesh defines the discrete control volumes over which the governing equations are solved. Unlike numerical parameters that can often be adjusted during a simulation, mesh-related errors are embedded in the solution from the start and cannot be corrected later.

A poor mesh will not simply reduce accuracy; it can fundamentally change the physics that the solver is capable of representing. No turbulence model, discretization scheme, or solver setting can compensate for insufficient or inconsistent spatial resolution.

---

## 4.2 Mesh Design as a Physical Problem

Mesh design must begin from the **physics of the flow**, not from geometric convenience.

Key questions that should guide mesh strategy include:
- Where are large gradients expected (velocity, pressure, volume fraction)?
- What length scales control the flow (boundary layers, shear layers, wakes, interfaces)?
- Is the flow steady or transient, and what spatial resolution is required to capture temporal behavior?

The mesh must be refined in regions where the governing equations exhibit strong gradients or where modeled physics (e.g. turbulence closure or interface tracking) impose resolution requirements.

---

## 4.3 Resolution Requirements and Non-Dimensional Considerations

Mesh resolution should be evaluated using **non-dimensional metrics**, not absolute cell size.

For wall-bounded turbulent flows, near-wall resolution is commonly characterized using the non-dimensional wall distance:

\[
y^+ = \frac{u_\tau y}{\nu}
\]

where \(u_\tau\) is the friction velocity, \(y\) the wall-normal distance to the first cell center, and \(\nu\) the kinematic viscosity.

Typical guidelines:
- Low-Re RANS / LES: \(y^+ \approx 1\)
- Wall-function RANS: \(30 < y^+ < 300\)

These values are **model-dependent** and must be consistent with the chosen turbulence treatment.

---

## 4.4 Mesh Quality Metrics in OpenFOAM

OpenFOAM evaluates mesh quality using several geometric metrics, accessible via `checkMesh`. The most critical are:

- **Non-orthogonality**  
- **Skewness**  
- **Aspect ratio**  
- **Cell volume variation**

While OpenFOAM can tolerate relatively high non-orthogonality through corrected discretization schemes, excessive values increase numerical diffusion and instability. Mesh quality limits should be interpreted as **risk indicators**, not pass/fail criteria.

---

## 4.5 Structured vs Unstructured Meshes

Structured meshes (e.g. `blockMesh`) provide excellent numerical properties and control over resolution, but are often impractical for complex geometries.

Unstructured meshes (e.g. `snappyHexMesh`) offer geometric flexibility but require careful attention to:
- Surface refinement consistency
- Boundary layer resolution
- Transition between refinement levels

The choice should be driven by the required physics, not mesh generation convenience.

---

## 4.6 Boundary Layer Resolution

Accurate prediction of wall-bounded flows requires explicit attention to boundary layer resolution.

Key considerations:
- Number of cells across the boundary layer
- Growth rate of wall-normal cell spacing
- Consistency with turbulence model assumptions

Excessive growth rates or insufficient wall-normal resolution often lead to unphysical wall shear stress and pressure loss predictions.

Near-wall mesh resolution must be consistent with the turbulence model; see
Chapter 6 — Near-Wall Treatment and y⁺.

---

## 4.7 Mesh-Induced Failure Modes

Common mesh-related failure modes include:
- Spurious pressure oscillations due to skewed cells  
- Unstable volume fraction transport in VOF simulations  
- Excessive numerical diffusion in shear layers  
- Apparent convergence to physically incorrect solutions  

These failures may not produce solver errors but manifest as non-physical results.

---

## 4.8 Mesh Verification and Independence

Mesh independence is not demonstrated by arbitrary refinement. Instead, refinement must target **physically relevant regions** and monitored quantities.

Verification strategies include:
- Systematic refinement studies
- Monitoring integral quantities (forces, fluxes)
- Comparing local profiles at critical sections

Mesh convergence should be interpreted in the context of modeling uncertainty, not as an absolute guarantee of accuracy.

---

## 4.9 Practical Recommendations

- Design the mesh after selecting the solver and turbulence model  
- Refine where physics demands it, not everywhere  
- Use `checkMesh` as a diagnostic, not a certification  
- Prefer simpler meshes with known behavior over complex meshes of uncertain quality  

A mesh is successful when it enables the solver to represent the intended physics stably and transparently.
