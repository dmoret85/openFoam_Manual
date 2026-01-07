# Incompressible Engineering Case Template

This directory provides a **baseline OpenFOAM case template** for incompressible flows.
It is intended as a **robust starting point** for engineering simulations, not as a
performance-optimized or tutorial case.

The template prioritizes:
- Physical consistency
- Numerical stability
- Transparency of assumptions
- Reproducibility

---

## 1. Engineering Objective

**Describe the engineering question being answered.**

Examples:
- Pressure drop across a component
- Velocity distribution in a channel
- Forces acting on a body

Clearly state what quantities will be extracted and how they will be used.

---

## 2. Physical Assumptions

Document all major assumptions explicitly.

- Flow regime: incompressible
- Fluid: Newtonian
- Density and viscosity: constant
- Gravity: on / off
- Steady or transient: (state clearly)

This case uses wall-function RANS.
Target near-wall resolution: 30 < y⁺ < 300
(see Chapter 6 — Near-Wall Treatment and y⁺).

If an assumption is questionable, document why it is still acceptable.

---

## 3. Turbulence Modeling

- Turbulence model: (e.g. laminar, RANS, LES)
- Near-wall treatment: (wall functions / wall-resolved)
- Target wall resolution: (e.g. y⁺ range)

The mesh **must be consistent** with the turbulence model choice.

---

## 4. Boundary Conditions

Summarize boundary conditions in physical terms.

- Inlet: velocity / mass flow / profile
- Outlet: pressure reference
- Walls: no-slip

Boundary condition selection follows **Chapter 7 — Boundary Conditions** (see `07_boundary_conditions/`), especially `outlets.md` for backflow-safe outlet handling.
