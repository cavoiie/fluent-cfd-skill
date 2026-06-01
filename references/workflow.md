# Fluent Workflow

Use this reference to keep Fluent work in a reproducible order.

## Task Routing

- Planning or model choice: read `solver-selection.md`, then turbulence or boundary references as needed.
- Case review: inspect mesh/setup assumptions, then read `validation-checklist.md`.
- Running a case: read `pyfluent-mcp.md` and `numerics-and-convergence.md`.
- Diagnosing failures: read `error-recovery.md`, then the specific reference for the failing subsystem.
- Post-processing or trust assessment: read `validation-checklist.md`.

## Minimum Case Definition

Capture these facts before recommending solver settings:

- Purpose: drag, pressure drop, heat transfer, mixing, separation, mass flow, acoustic/noise proxy, or another objective.
- Regime: steady/transient, incompressible/compressible, laminar/turbulent, single/multiphase, reacting/non-reacting.
- Geometry and scale: characteristic length, boundary names, rotating/moving parts, symmetry or periodicity.
- Fluid/materials: density model, viscosity model, temperature dependence, compressibility, phase properties.
- Boundary data: mass/velocity/pressure/temperature/turbulence inputs and expected outlet behavior.
- Validation evidence: experiment, analytical estimate, literature, mesh independence, conservation, or engineering target.

## Standard Execution Sequence

1. Confirm units and scale before assigning physics.
2. Check zones and boundary names before writing or running commands.
3. Check mesh quality and wall resolution before judging turbulence results.
4. Initialize with a physically plausible field.
5. Run a short smoke test.
6. Review residuals, warnings, reversed flow, and monitor movement.
7. Continue only when the smoke run is numerically stable.
8. Save case/data after meaningful setup changes or a converged/accepted state.

## Reporting

End with:

- What was changed or checked.
- Whether the case is runnable, converged, or validated.
- Evidence used: residuals, monitors, conservation, mesh checks, or comparison target.
- Remaining risks and the next smallest action.

