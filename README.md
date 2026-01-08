# OpenFOAM Engineering Manual

The **OpenFOAM Engineering Manual** is an engineering-focused guide that bridges the gap between official OpenFOAM documentation and real-world CFD practice. It explains *why* modelling and numerical choices are made, *how* to detect failure modes, and *how* to build stable, physically consistent simulations.

This manual is written for engineers who use OpenFOAM as a **decision-making tool**, not just a solver.

---

## Purpose

This repository documents practical, engineering-level knowledge for using OpenFOAM as a reliable CFD tool.  
It focuses on **reasoning, assumptions, diagnostics, and verification**, rather than tutorial-style repetition of syntax.

The emphasis is on:
- understanding modelling choices
- designing numerically stable cases
- diagnosing incorrect but converged solutions
- establishing confidence in results

---

## Scope

The manual primarily addresses:

- Incompressible and weakly compressible flows  
- Transient simulations and numerical stability  
- Turbulence modelling (RANS, LES, hybrid approaches)  
- Free-surface and multiphase flows  
- Mesh strategy and mesh quality control  
- Boundary conditions and physical consistency  
- Verification, validation, and post-processing  
- Debugging and common CFD failure modes  

---

## What This Manual Is Not

- Not a replacement for official OpenFOAM documentation  
- Not a collection of copy-paste tutorials  
- Not an introduction to basic fluid mechanics or numerical methods  

Readers are expected to consult official documentation for solver syntax and implementation details.

---

## Philosophy

**Engineering-first, solver-aware, and opinionated where necessary.**

Assumptions and limitations are stated explicitly.  
Recommendations are justified using physics, numerics, and observed failure patterns rather than convention.

This manual prioritizes **robustness and credibility** over minimal runtime or academic novelty.

---

## Status

🚧 **Work in progress** — structure is stabilizing, content will continue to evolve.

---

## Table of Contents

### Chapter 01 — Introduction
- [01.1 Philosophy](01_introduction/01.1_Philosophy.md)
- [01.2 How This Manual Differs](01_introduction/01.2_How_this_manual_differs.md)
- [01.3 Scope, Assumptions, and Limitations](01_introduction/01.3_Limitations_and_scope.md)

---

### Chapter 04 — Mesh Strategy and Quality
- [04.1 Mesh Strategy](04_Mesh%20Strategy%20and%20Quality/04.1_Mesh_strategy.md)
- [04.2 Mesh Quality Metrics](04_Mesh%20Strategy%20and%20Quality/04.2_Mesh_quality_metrics.md)

---

### Chapter 06 — Turbulence Modelling
- [06.1 Turbulence Overview](06_Turbulence%20Modelling/06.1_Turbulence_overview.md)
- [06.2 Near-Wall Treatment and y⁺](06_Turbulence%20Modelling/06.2_Near_wall_treatment.md)
- [06.3 Turbulence Model Selection](06_Turbulence%20Modelling/06.3_Model_selection.md)

---

### Chapter 07 — Boundary Conditions
- [07.1 Physical Consistency](07_Boundary%20conditions/07.1_Physical_consistency.md)
- [07.2 Inlets](07_Boundary%20conditions/07.2_Inlets.md)
- [07.3 Outlets](07_Boundary%20conditions/07.3_Outlets.md)
- [07.4 Walls and Symmetry](07_Boundary%20conditions/07.4_Walls_and_symmetry.md)

---

### Chapter 08 — Numerics and Stability
- [08.1 Numerics and Stability](08_Numerics%20and%20Stability/08.1_Numerics_and_stability.md)
- [08.2 Time-Step Control](08_Numerics%20and%20Stability/08.2_Time_step_control.md)
- [08.3 fvSchemes Best Practices](08_Numerics%20and%20Stability/08.3_FvSchemes_best_practices.md)

---

### Chapter 10 — Verification and Validation
- [10.1 Verification](10_Verification%20and%20Validation/10.1_Verification.md)
- [10.2 Validation](10_Verification%20and%2_)

## Chapter 12 - Debugging and Troubleshooting

## Chapter 13 - Case Library
