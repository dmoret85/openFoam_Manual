# Chapter 08 — Numerics and Stability

Numerical stability is a prerequisite for physically meaningful CFD results.
A simulation that converges numerically may still be wrong, but a simulation
that is numerically unstable cannot be trusted at all.

This chapter explains how numerical choices in OpenFOAM affect stability,
accuracy, and robustness, with emphasis on engineering practice rather than
solver theory.

## Contents

- Section 08.1 — Numerical stability and failure modes
- Section 08.2 — Time-step control and CFL
- Section 08.3 — Spatial discretisation and `fvSchemes`

The focus is on understanding *why* simulations fail or converge incorrectly,
and how to design numerics that are consistent with mesh quality and physics.
