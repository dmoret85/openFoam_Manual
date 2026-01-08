# Engineering Examples

This folder contains **worked, problem-specific OpenFOAM cases** that demonstrate
end-to-end engineering CFD workflows, including:

- problem formulation and assumptions
- mesh strategy and quality checks
- turbulence modelling and near-wall treatment
- boundary conditions and physical consistency
- numerics, stability, and convergence behaviour
- verification (mesh/time-step sensitivity)
- validation where suitable reference data exists

These examples are intentionally **case-specific** and may include choices that
are not appropriate as general defaults.

## Relationship to the Case Template

General, reusable starting points live in:
- `../_case_template_incompressible/` (generic template)

Engineering examples should reference relevant manual chapters and explain
the reasoning behind all modelling and numerical decisions.
