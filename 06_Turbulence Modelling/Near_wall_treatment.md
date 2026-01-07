# Near-Wall Treatment and y⁺

Near-wall treatment is a core assumption in turbulence modeling. The choice between wall functions and wall-resolved approaches determines the required mesh resolution near solid boundaries and directly affects solution validity.

The non-dimensional wall distance y⁺ is used to assess whether the mesh resolution near walls is consistent with the selected turbulence model.

---

## 1. Definition of y⁺

The non-dimensional wall distance is defined as:

y⁺ = (u_τ y) / ν

where:
- u_τ is the friction velocity
- y is the distance from the wall to the center of the first cell
- ν is the kinematic viscosity

y⁺ measures how well the near-wall region is resolved relative to viscous effects.

---

## 2. y⁺ Ranges and Modeling Assumptions

### Wall-function approaches (engineering default)

For RANS simulations using wall functions (e.g. k–ω SST with wall functions):

- Target range: **30 < y⁺ < 300**
- The viscous sublayer is not resolved
- Wall shear stress is modeled

This approach is robust and computationally efficient, but relies on correct y⁺ placement.

---

### Wall-resolved approaches (low-Re / LES)

For wall-resolved RANS or LES:

- Target range: **y⁺ ≈ 1**
- The viscous sublayer is explicitly resolved
- Requires very fine near-wall meshes

This approach is significantly more expensive and sensitive to mesh quality.

---

## 3. Computing y⁺ in OpenFOAM

In OpenFOAM RANS simulations, y⁺ can be computed using:

- The `yPlusRAS` utility, or
- A `yPlusRAS` function object during runtime

y⁺ should be evaluated after the initial transient, once turbulence has developed.

---

## 4. Interpreting y⁺ Results

### y⁺ too low for wall functions
If y⁺ is significantly below the target range while using wall functions, the near-wall model assumptions are violated and results may be unreliable.

### y⁺ too high
Excessively large y⁺ values indicate insufficient near-wall resolution and poor prediction of wall shear stress.

### Strong spatial variation
Large variations in y⁺ often indicate mesh transitions or inadequate boundary layer meshing.

---

## 5. Engineering Guidance

- Select the turbulence model before meshing
- Design the near-wall mesh to match the model assumptions
- Use y⁺ as a **consistency check**, not a tuning parameter
- Document the target y⁺ range explicitly

A simulation is only valid if its near-wall resolution is consistent with its turbulence model.
