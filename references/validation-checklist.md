# Validation Checklist

Use this reference before claiming a Fluent result is usable.

## Setup Integrity

- Units and dimensions are correct.
- Materials and property models match the intended regime.
- Boundary conditions match known physical inputs.
- Reference values are set correctly for coefficients.
- Mesh zones and interfaces match the geometry and physics.

## Mesh Quality

- Skewness, orthogonal quality, aspect ratio, and non-orthogonality are acceptable for the solver and model.
- Boundary-layer mesh supports the wall treatment and y+ target.
- Important gradients have local resolution.
- A mesh-independence plan exists for final results.

## Conservation

- Net mass imbalance is checked and reported.
- Energy imbalance is checked when the energy equation is active.
- Phase conservation is checked for multiphase cases.
- Forces, fluxes, and source terms are consistent with expected signs and magnitudes.

## Convergence and Monitoring

- Residuals are only one piece of evidence.
- Objective monitors stabilize or reach periodic/statistical stationarity.
- Key fields show physically plausible distributions.
- Warnings are explained or resolved.

## Result Review

- Compare against an estimate, experiment, literature, previous simulation, or simplified calculation when possible.
- Check sensitivity to mesh, time step, turbulence model, and boundary assumptions for final claims.
- Report uncertainty and unresolved risks instead of overstating precision.

## Minimum Acceptance Statement

Use a concise status:

- "Runnable": setup starts and smoke run is stable.
- "Numerically converged": residuals, monitors, and balances meet criteria.
- "Physically validated": result has comparison evidence or sensitivity checks.
- "Not trusted": list the blocking issue and next correction.

