# Engineering Examples

This directory contains **worked, problem-specific OpenFOAM cases** that
demonstrate how the principles in the *OpenFOAM Engineering Manual* are applied
in practice.

Each example represents a complete engineering workflow, including:

* problem formulation and assumptions
* mesh strategy and quality assessment
* turbulence modelling and near-wall treatment
* boundary conditions and physical consistency
* numerical stability and convergence behaviour
* verification and, where applicable, validation
* diagnosis of common failure modes

These cases are intended for **learning, reference, and verification**, not as
generic starting points.

---

## Relationship to the Case Template

Reusable baseline setups are provided separately in:

```
_case_template_incompressible/
```

The template prioritizes robustness and transparency and should be used as the
starting point for new simulations.
Engineering examples may build upon the template but include **case-specific
choices** that are not suitable as general defaults.

---

## Using the Examples

Readers are encouraged to:

* compare modelling choices against the manual chapters
* modify parameters deliberately and observe consequences
* use examples as verification benchmarks

Each example explicitly references relevant manual chapters to maintain traceability.
