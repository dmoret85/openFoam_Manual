# Turbulent Channel Flow — Engineering Example

This example presents a **worked engineering CFD case** for fully developed turbulent flow in a plane channel using OpenFOAM.

The purpose of this case is not to demonstrate solver usage or achieve optimal performance, but to **demonstrate how the principles of the OpenFOAM Engineering Manual are applied in practice**, from problem formulation through verification and diagnosis.

---

## 1. Engineering Objective

The primary objectives of this case are to:

* Predict the mean velocity profile across the channel
* Estimate wall shear stress and friction velocity
* Assess numerical stability and model consistency for a canonical turbulent flow

The broader objective is to answer:

> *Can a RANS-based OpenFOAM simulation produce physically consistent results when modelling, meshing, and numerics are chosen deliberately and verified?*

---

## 2. Physical Description and Assumptions

### Flow description

* Incompressible turbulent flow
* Fully developed in the streamwise direction
* Statistically steady
* Driven by an imposed pressure gradient or equivalent forcing

### Key assumptions

* Constant fluid properties
* No heat transfer
* No buoyancy or body forces
* No transition modeling

These assumptions follow the guidance in:

* **Chapter 01 — Introduction**
* **Section 01.3 — Limitations and scope**

---

## 3. Governing Equations and Turbulence Modelling

### Flow model

* Incompressible Navier–Stokes equations
* Reynolds-averaged formulation (RANS)

### Turbulence model

* k–ω SST with wall functions

### Near-wall treatment

* Wall-function approach
* Target near-wall resolution: **30 < y⁺ < 300**

Modelling choices are guided by:

* **Chapter 06 — Turbulence Modelling**
* **Section 06.2 — Near-Wall Treatment **
* **Section 06.3 — Model Selection**

---

## 4. Geometry and Mesh Strategy

### Geometry

* Plane channel of height *H*
* Streamwise length chosen to avoid outlet influence
* Spanwise direction treated as 2D or periodic

### Mesh strategy

* Structured, body-aligned mesh
* Wall-normal refinement to resolve boundary layers
* Gradual cell size transitions

Mesh design and quality assessment follow:

* **Section 04.1 — Mesh Strategy**
* **Section 04.2 — Mesh Quality Metrics**

Near-wall spacing is selected based on the chosen turbulence model, not adjusted post hoc.

---

## 5. Boundary Conditions

Boundary conditions are selected to avoid over-constraint and ensure physical consistency:

* Velocity:

  * Inlet: prescribed bulk velocity or mass flow
  * Walls: no-slip
* Pressure:

  * Outlet or reference pressure treatment consistent with fully developed flow

Boundary condition guidance follows:

* **Chapter 07 — Boundary Conditions**
* **Section 07.3 — Outlets**

---

## 6. Numerical Strategy

The simulation is treated as **transient**, even though the target solution is statistically steady.

Numerical choices include:

* CFL-controlled time stepping
* Conservative, bounded spatial discretization during startup
* Gradual increase in numerical accuracy only after stability is demonstrated

Numerical guidance follows:

* **Chapter 08 — Numerics and Stability**
* **Section 08.2 — Time-Step Control**
* **Section 08.3 — fvSchemes Best Practices**

---

## 7. Verification Approach

Verification is performed before any validation claims.

Planned verification steps:

* Mesh refinement study (wall-normal resolution)
* Time-step sensitivity study
* Monitoring of:

  * Mass balance
  * Wall shear stress
  * Mean velocity profile stability

Verification methodology follows:

* **Chapter 10 — Verification and Validation**
* **Section 10.1 — Verification**

---

## 8. Validation Reference

Validation is performed against:

* Expected log-law behavior in wall units
* Published DNS data for turbulent channel flow (where applicable)

Validation focuses on **trends and consistency**, not exact pointwise agreement.

Guidance follows:

* **Section 10.2 — Validation**

---

## 9. Diagnostics and Debugging

Common issues encountered in this type of case include:

* Incorrect near-wall resolution (y⁺ mismatch)
* False convergence in steady-state approximations
* Pressure–velocity coupling sensitivity

Debugging strategy follows:

* **Chapter 12 — Debugging and Troubleshooting**
* Especially **Section 12.6 — False Convergence**

---

## 10. Quantities of Interest

Primary monitored quantities include:

* Bulk velocity
* Wall shear stress
* Friction velocity (uτ)
* Mean velocity profile across the channel

Residuals are monitored as numerical indicators but are not used as the sole convergence criterion.

---

## 11. Expected Outcome

A successful simulation should demonstrate:

* Stable numerical behavior
* Reasonable y⁺ distribution
* Physically plausible velocity profiles
* Insensitivity to small numerical changes

Perfect agreement with reference data is not expected; **physical consistency and robustness** are the primary goals.

---

## 12. Role of This Case

This example is intended to serve as:

* A reference implementation of the manual’s principles
* A verification benchmark for new OpenFOAM setups
* A diagnostic case for numerical and modeling behavior

Users are encouraged to modify modeling and numerical choices deliberately and observe the consequences using the manual as guidance.

---

## Engineering Rule

> **Do not pursue accuracy or performance before establishing numerical stability and physical consistency.**

