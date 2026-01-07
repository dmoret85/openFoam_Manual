# Chapter 1 — Philosophy and Scope

## 1.1 Purpose of This Manual

This manual is written to support the **engineering use of OpenFOAM**, not merely its operation.

OpenFOAM is a powerful and flexible CFD framework, but its flexibility places a large burden on the user. Many simulations run without errors while producing results that are numerically unstable, physically inconsistent, or simply meaningless from an engineering perspective. Official documentation and tutorials explain how to execute solvers, but often do not explain how to design a simulation that can be trusted.

The purpose of this manual is to document the **reasoning process** behind OpenFOAM simulations: how to translate a physical problem into a mathematical model, how to choose solvers and numerical methods, and how to evaluate whether the results are credible.

---

## 1.2 Target Audience

This manual is intended for:

- Graduate students with prior CFD coursework  
- Researchers using OpenFOAM for applied fluid mechanics  
- Practicing engineers performing CFD for design or analysis  

The reader is assumed to have a basic understanding of:
- Fluid mechanics
- Partial differential equations
- Numerical methods for CFD

This is **not** an introductory text on fluid mechanics or numerical analysis.

---

## 1.3 Engineering-Centered Approach

The guiding principle of this manual is:

> **A CFD simulation is an engineering model, not a numerical experiment.**

Every OpenFOAM case represents a set of assumptions:
- Physical (e.g. incompressibility, turbulence closure)
- Mathematical (e.g. averaged equations, interface modeling)
- Numerical (e.g. discretization schemes, time integration)

These assumptions are always present, whether acknowledged or not. This manual makes them **explicit**, discusses their implications, and explains how they influence accuracy, stability, and interpretability.

---

## 1.4 What This Manual Emphasizes

This manual emphasizes:

- Physical consistency of boundary and initial conditions  
- Appropriate solver and turbulence model selection  
- Mesh resolution requirements tied to flow physics  
- Numerical stability and time-step control  
- Interpretation of residuals and convergence behavior  
- Identification of common failure modes  

Where possible, guidance is framed in terms of **engineering decision-making**, not solver-specific recipes.

---

## 1.5 What This Manual Does Not Attempt

This manual does not aim to:

- Replace official OpenFOAM user or programmer documentation  
- Provide exhaustive reference material for all solvers  
- Serve as a collection of tutorial cases  
- Teach basic CFD or fluid mechanics theory  

Official documentation, source code, and community resources are referenced where appropriate and should be considered complementary.

---

## 1.6 OpenFOAM Versions and Scope

The primary reference platform for this manual is **OpenFOAM Foundation (v9 and later)**.  
Where relevant, differences with **ESI-OpenCFD** versions are noted explicitly.

The technical focus is on:
- Incompressible and weakly compressible flows  
- Transient simulations  
- Turbulence modeling (RANS, LES, hybrid approaches)  
- Free-surface and multiphase flows using VOF  

Compressible, reacting, and highly specialized solvers are outside the primary scope unless stated otherwise.

---

## 1.7 How to Use This Manual

This manual is designed to be read **non-linearly**. Chapters are largely self-contained and can be used as references during case setup, debugging, or result interpretation.

Readers are encouraged to:
- Question default settings
- Inspect numerical behavior critically
- Validate results against physical expectations

The goal is not to run OpenFOAM successfully, but to **know when to trust it**.
