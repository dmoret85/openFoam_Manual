# Chapter 6 — Turbulence modelling

# Turbulence Modelling — Engineering Perspective

Turbulence modelling is a core part of the mathematical model in CFD, not a numerical option. In most engineering flows, the governing equations are solved in an averaged or filtered form, and turbulence models are required to close the system.

A turbulence model does not introduce turbulence into the flow. It represents the effect of unresolved turbulent motion on the resolved scales. As such, turbulence modelling introduces **physical assumptions** that cannot be eliminated by numerical refinement alone.

---

## 1. Averaged and Filtered Flow Descriptions

Turbulence models arise from modifying the Navier–Stokes equations:

- **RANS (Reynolds-Averaged Navier–Stokes)**  
  Governing equations are time-averaged. All turbulent scales are modelled.

- **LES (Large Eddy Simulation)**  
  Governing equations are spatially filtered. Large scales are resolved; small scales are modelled.

- **Hybrid RANS–LES**  
  Combine RANS behavior near walls with LES-like behavior in separated regions.

Each approach implies different resolution requirements, computational cost, and predictive capability.

---

## 2. RANS modelling in Engineering Practice

RANS models are the most widely used approach in engineering CFD due to their robustness and efficiency.

They are well suited for:
- Steady or statistically steady flows
- Design-oriented simulations
- Flows dominated by attached boundary layers

RANS models assume a clear separation between mean flow and turbulent fluctuations. They may struggle in flows with strong unsteadiness, separation, or transition.

---

## 3. LES and Resolution Dependence

LES resolves a portion of the turbulence spectrum and therefore places strict demands on mesh resolution and time stepping.

LES is appropriate when:
- Large-scale unsteadiness is essential to the problem
- Transient flow structures are of interest
- Computational resources are sufficient

LES performed on an under-resolved mesh degenerates into an expensive and poorly controlled model and should be avoided.

---

## 4. Hybrid Approaches

Hybrid RANS–LES models aim to balance cost and fidelity but are sensitive to:
- Mesh density and anisotropy
- Transition regions between RANS and LES behavior
- Flow separation location

These models require careful validation and should not be treated as general-purpose solutions.

---

## 5. Turbulence modelling as an Assumption

Turbulence modelling choices define what physics the simulation can and cannot represent.

Key points:
- A more complex model does not guarantee better results
- Model choice must be consistent with mesh resolution
- Turbulence models must be selected **before** meshing

Turbulence modelling should be treated as an explicit modelling assumption and documented accordingly.
