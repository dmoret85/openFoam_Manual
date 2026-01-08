# Mesh Strategy — Turbulent Channel Flow

This document describes the **mesh design rationale** for the turbulent channel flow engineering example.
The mesh is designed to be **physically consistent with the turbulence model**, numerically robust, and suitable for verification studies.

Mesh decisions are made **before** solver or numerical tuning, following the principles outlined in the *OpenFOAM Engineering Manual*.

---

## 1. Mesh Objectives

The primary objectives of the mesh are to:

* Resolve near-wall regions consistently with wall-function assumptions
* Maintain good cell alignment with the dominant flow direction
* Minimize numerical diffusion and instability
* Enable systematic mesh refinement for verification

The mesh is not optimized for minimal cell count, but for **predictable numerical behavior**.

---

## 2. Geometry Overview

The domain represents a **plane channel** with:

* Height: *H*
* Streamwise length: *L* ≫ *H* (to minimize outlet influence)
* Spanwise direction: treated as 2D or periodic

Walls are located at the top and bottom boundaries and are the primary regions of interest for mesh refinement.

---

## 3. Mesh Topology

A **structured, body-aligned mesh** is used.

Rationale:

* The geometry is simple and canonical
* Structured meshes provide predictable quality
* Alignment with the flow minimizes numerical diffusion

The mesh is intended to be generated using `blockMesh`.

---

## 4. Near-Wall Resolution and y⁺ Target

### Turbulence model assumption

* RANS
* k–ω SST with wall functions

### y⁺ strategy

* Wall-function approach
* Target range: **30 < y⁺ < 300**

The first cell height is chosen based on:

* Estimated friction velocity
* Kinematic viscosity
* Expected bulk velocity

The mesh is designed so that **y⁺ falls within the target range by construction**, not by numerical tuning.

Near-wall treatment guidance follows:

* **Section 06.2 — Near-Wall Treatment and y⁺**

---

## 5. Wall-Normal Refinement Strategy

* Fine resolution near walls
* Gradual growth rate away from the wall
* Avoid abrupt jumps in cell size

The growth rate is selected to balance:

* resolution of velocity gradients
* numerical stability
* reasonable aspect ratios

Abrupt transitions are avoided to reduce numerical stiffness.

---

## 6. Aspect Ratio Considerations

High aspect ratio cells are expected and acceptable near the walls.

Engineering interpretation:

* High aspect ratio is not inherently problematic
* Cell alignment with the flow is critical
* Problems arise when high aspect ratio is combined with:

  * poor alignment
  * skewness
  * non-orthogonality

Aspect ratio is therefore evaluated **in context**, not as a standalone metric.

---

## 7. Mesh Quality Expectations

Mesh quality is assessed using `checkMesh`.

Key metrics of interest:

* Non-orthogonality
* Skewness
* Aspect ratio
* Cell volume variation

Quality limits are interpreted as **risk indicators**, not pass/fail criteria, following:

* **Section 04.2 — Mesh Quality Metrics**

Special attention is paid to mesh quality near the walls, where gradients are strongest.

---

## 8. Planned Mesh Sensitivity Study

The mesh is designed to support systematic refinement:

* Increase wall-normal resolution
* Adjust first cell height
* Refine streamwise resolution if required

Mesh sensitivity results are documented as part of:

* **Section 10.1 — Verification**

Refinement decisions are based on changes in **quantities of interest**, not local point values alone.

---

## 9. Relationship to Numerical Schemes

The initial mesh is designed to be compatible with:

* conservative, bounded discretization schemes
* moderate CFL limits

Higher-order schemes are introduced **only af
