# Turbulence and Wall Treatment

Use this reference when selecting turbulence models, wall treatment, and mesh requirements.

## Decide Laminar vs Turbulent

Estimate Reynolds number and flow features. Laminar may be appropriate for low-Re internal flows or microflows, but transitional and separated cases need explicit justification.

## Model Selection

- Spalart-Allmaras: external aerodynamic boundary layers and efficient attached-flow studies; weaker for strong separation or complex recirculation.
- k-epsilon family: robust industrial default for many free-shear and fully turbulent internal flows; less accurate near adverse pressure gradients and separation.
- Realizable/RNG k-epsilon: often better than standard k-epsilon for strain, swirl, and recirculation, but still depends on wall treatment.
- k-omega SST: strong default for adverse pressure gradient, separation, near-wall sensitivity, turbomachinery, and aerodynamic cases.
- Reynolds Stress Model: consider for strong anisotropy, swirl, secondary flows, or curvature when simpler eddy-viscosity models fail.
- LES/DES/SAS: use only with transient setup, suitable mesh/time step, and enough compute budget.

## Wall Resolution

- Wall functions generally require y+ in a wall-function-compatible range and adequate boundary-layer mesh.
- Low-Re / enhanced wall treatment requires near-wall cells fine enough to resolve the viscous sublayer.
- SST performance depends strongly on near-wall mesh quality and prism/inflation layers.

## Required Checks

- State the expected y+ target before solving.
- Check inflation layers, growth ratio, first-cell height, and skewness near walls.
- Tie turbulence inlet quantities to physical estimates, not arbitrary defaults.
- For heat transfer, ensure thermal boundary layer resolution is adequate.

## Guardrails

- Do not switch models just to force convergence.
- Do not compare turbulence models without keeping mesh, numerics, and monitors controlled.
- Do not trust wall shear, heat transfer, or drag results without wall-resolution evidence.

