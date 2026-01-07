# Outlets

Outlet boundary conditions must allow the flow to leave the domain without artificially constraining the solution. In incompressible OpenFOAM solvers, the outlet is also the most common place to define a **pressure reference**.

## 1. Pressure reference requirement

In incompressible flow, pressure is defined up to a constant. The system requires one reference, typically:
- Fix `p` at the outlet (most common engineering practice)

This avoids drift in the pressure field and provides a stable closure for pressure–velocity coupling.

## 2. Recommended baseline pairing

A robust default pairing is:

| Patch  | U            | p           |
|--------|--------------|-------------|
| inlet  | fixedValue   | zeroGradient|
| outlet | zeroGradient | fixedValue  |
| walls  | noSlip       | zeroGradient|

This pairing avoids over-constraint and is stable for many internal-flow setups.

## 3. Backflow and recirculation at outlets

If recirculation reaches the outlet, `zeroGradient` for `U` can behave poorly because backflow may introduce non-physical values.

In such cases, use a backflow-safe outlet velocity condition:

### Backflow-safe outlet for U
- `inletOutlet` applies `zeroGradient` for outflow
- switches to a specified `inletValue` during backflow

This prevents undefined or unstable behavior when flow reverses locally.

## 4. When not to trust the outlet

If you see:
- sustained backflow at the outlet
- strong gradients or separation close to the boundary
- sensitivity of forces/pressure-drop to outlet position

then the outlet boundary is influencing the physics. Extend the domain or change the boundary placement.

## 5. Common mistakes

Avoid:
- fixing pressure at multiple boundaries (over-constraint)
- fixing both `U` and `p` at the same boundary without justification
- using `fixedFluxPressure` by default (use only when you understand why)
- placing an outlet too close to a separated region
