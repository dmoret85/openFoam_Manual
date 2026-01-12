# Chapter 05 — Solver Selection and Usage

Solver selection is one of the most frequent sources of silent error in CFD practice: a solver may run to completion, suppress residuals, and still produce results that do not represent the physics of interest. In this chapter, we focus on *how to choose the correct solver for a given engineering problem* and *why* that choice matters in practice.

This chapter assumes the reader has basic familiarity with OpenFOAM case structure and physics assumptions (see Chapters 02–04) and will link solver choice to modelling objectives, stability considerations, and validation practices (see Chapters 08 and 10).

---

## 5.1 Solver Families and Classification

OpenFOAM provides many solver applications. Each solver embodies a set of assumptions about the physics it resolves and the numerical algorithms it uses. From an engineering perspective, understanding these assumptions is critical to ensuring that the solver addresses the *dominant physics* in the problem rather than numerical artefacts.

The classification below groups solvers by the *physics they capture*, rather than by name alone. This aligns with the engineering workflow where the *physical question defines the solver*, not the other way around.

### 5.1.1 Incompressible Flow Solvers
These solvers assume constant density and negligible compressibility effects. They are appropriate when density variations are not central to the engineering question (e.g., incompressible water flow in pipes or channels).

Typical solvers in this group include:
- `simpleFoam` — for steady-state incompressible flows.
- `pisoFoam` — for transient incompressible flows.
- `pimpleFoam` — for flexible transient/steady hybrid control.

This class is often used for internal and external flows where *free surfaces and compressibility are secondary or absent*.

For precise syntax or solver flags, consult the official OpenFOAM user guide. :contentReference[oaicite:5]{index=5}

---

### 5.1.2 Free-Surface and Multiphase Solvers
When interface dynamics (e.g., air–water interaction) are central to the engineering question, incompressible solvers are insufficient. Solvers in this group explicitly transport phase fractions and model surface physics.

Common examples:
- `interFoam`
- `interIsoFoam`
- `multiphaseEulerFoam`

These solvers model the physics of multiple phases and interfaces. They *must* be treated as inherently transient and *numerically sensitive* — consistent with the requirements described in Chapters 08 and 09. :contentReference[oaicite:6]{index=6}

---

### 5.1.3 Compressible Solvers
These solvers allow density to vary with pressure, temperature, or composition. Compressibility is significant only when the flow physics requires it (e.g., high-speed gases, strong thermal gradients). For many civil and water engineering applications, compressibility effects are negligible; using compressible solvers without justification increases numerical cost and instability.

Examples:
- `rhoSimpleFoam`
- `rhoPimpleFoam`

See the official docs for detailed syntax and variable definitions. :contentReference[oaicite:7]{index=7}

---

### 5.1.4 Specialised and Extended Solvers
Certain solvers incorporate additional effects such as porous media resistance, sources, or coupled transport equations. These are built on the core families but add specific modelling assumptions. Users must understand any additional assumptions before choosing such solvers for design decisions.

Examples include porous or source-term augmented solvers provided by third-party libraries or custom builds.

---

