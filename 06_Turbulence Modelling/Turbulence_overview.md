# Chapter 6 — Turbulence Modeling

## 6.1 Role of Turbulence Modeling in Engineering CFD

Most engineering flows are turbulent, yet resolving all turbulent scales directly is computationally infeasible for practical problems. Turbulence models are therefore not optional approximations, but core components of the mathematical model.

A turbulence model does not “add turbulence” to the flow; it closes the governing equations by modeling the effect of unresolved scales. The quality of a CFD prediction depends on how well this closure aligns with the flow physics, mesh resolution, and numerical approach.

---

## 6.2 Averaged and Filtered Governing Equations

Turbulence modeling begins with a modification of the Navier–Stokes equations:

- **RANS** models operate on time-averaged equations  
- **LES** models operate on spatially filtered equations  
- **Hybrid models** blend both approaches  

Each framework introduces additional unknown terms that must be modeled. These modeled terms represent physical assumptions that cannot be removed by numerical refinement alone.

---

## 6.3 RANS Modeling: When and Why

Reynolds-Averaged Navier–Stokes (RANS) models are the most commonly used in engineering due to their robustness and low computational cost.

Typical use cases:
- Steady or statistically steady flows  
- Design studies requiring many simulations  
- Flows dominated by attached boundary layers  

RANS models assume a clear separation between mean flow and turbulent fluctuations. They are less reliable for strongly unsteady, separated, or transitional flows.

---

## 6.4 Near-Wall Treatment and Mesh Consistency

Near-wall treatment is inseparable from turbulence modeling.

Two common approaches:
- **Wall-resolved models**: require \(y^+ \approx 1\)  
- **Wall-function approaches**: valid for \(30 < y^+ < 300\)  

Using a turbulence model outside its intended near-wall resolution range produces physically inconsistent results, even if the solver converges.

---

## 6.5 LES Modeling: Capabilities and Requirements

Large Eddy Simulation (LES) resolves large turbulent structures while modeling subgrid-scale effects.

LES is appropriate when:
- Large-scale unsteadiness is important  
- Transient flow features dominate  
- Sufficient computational resources are available  

LES requires:
- Fine mesh resolution in all directions  
- Time steps small enough to resolve turbulence dynamics  
- Low numerical dissipation  

LES performed on an under-resolved mesh degenerates into an expensive RANS simulation with unpredictable behavior.

---

## 6.6 Hybrid RANS–LES Approaches

Hybrid models (e.g. DES, DDES) aim to combine RANS near walls with LES in separated regions.

These models are sensitive to:
- Grid spacing transitions  
- Mesh anisotropy  
- Flow separation location  

Hybrid approaches should be used with caution and only when their assumptions are well understood.

---

## 6.7 Turbulence Model Selection Strategy

Model selection should be driven by:
- Flow physics and dominant phenomena  
- Required accuracy and output quantities  
- Available mesh resolution and computational budget  

A more complex turbulence model does not guarantee better results. In many cases, a well-resolved RANS simulation is more reliable than a poorly resolved LES.

---

## 6.8 Common Turbulence-Related Failure Modes

Typical issues include:
- Using wall functions with \(y^+ \approx 1\)  
- Claiming LES with insufficient resolution  
- Interpreting RANS results as instantaneous flow  
- Ignoring turbulence model sensitivity  

These errors often produce smooth, apparently reasonable results that are physically misleading.

---

## 6.9 Engineering Guidance

- Choose turbulence models early, before meshing  
- Design the mesh to support the chosen model  
- Treat turbulence modeling as a modeling assumption, not a numerical setting  
- Validate turbulence predictions against physical expectations  

Turbulence modeling is a compromise between physics, numerics, and resources. Understanding that compromise is essential for trustworthy CFD.
