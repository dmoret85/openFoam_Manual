# Turbulence Model Selection — Engineering Workflow

Turbulence model selection should follow a structured decision process rather than habit or solver availability.

## 1. Identify the dominant flow features

Ask:
- Is the flow steady or inherently unsteady?
- Are separation and large-scale vortices important?
- Are wall quantities (shear, heat transfer) critical?

---

## 2. Match model complexity to available resolution

- Use **RANS** if the mesh cannot support LES-scale resolution
- Do not claim LES unless the mesh and time step are designed for it
- Prefer a well-resolved RANS model over an under-resolved LES

---

## 3. Near-wall strategy first, model second

Decide early:
- Wall functions → moderate near-wall resolution (y⁺ in log layer)
- Wall-resolved → fine near-wall resolution (y⁺ ≈ 1)

The mesh must be designed to support this decision.

---

## 4. Validate model behavior, not just convergence

Check:
- Sensitivity to turbulence model choice
- Physical plausibility of predicted trends
- Consistency with known flow behavior

A turbulence model is acceptable only if its assumptions remain valid for the problem being solved.
