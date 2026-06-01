# Numerics and Convergence

Use this reference for solver controls, initialization, monitors, and convergence assessment.

## Numerics

- Start with stable lower-order or default schemes only when needed for robustness; move to higher-order schemes for final engineering results when stable.
- Use coupled or pressure-velocity schemes appropriate to the flow stiffness, compressibility, and convergence behavior.
- Adjust under-relaxation factors only with a reason: oscillation, divergence, stiffness, or slow coupling.
- For transient cases, choose time step from physical time scales, Courant number, rotating speed, wave speed, or desired temporal resolution.

## Initialization

- Initialize from physically meaningful zones or hybrid initialization.
- Patch fields when needed for multiphase, temperature gradients, rotating regions, or known recirculation.
- Run a short smoke test before a long solve.

## Convergence Evidence

Require more than residuals:

- Residuals decrease and level at acceptable values for the model.
- Target monitors stabilize: force, pressure drop, heat rate, mass flow, averaged temperature, torque, or phase volume.
- Mass imbalance is small relative to total flow.
- Energy imbalance is checked when energy is active.
- Key contours and vectors are physically plausible.
- No unresolved warnings dominate the result: reversed flow, clipped variables, floating point exceptions, poor quality cells, or boundedness issues.

## Steady vs Transient

- Steady convergence: monitor values should stop drifting, not merely oscillate around a moving mean.
- Transient convergence: require periodic/statistical stationarity or time-window convergence; residuals per time step are not the final result.

## Red Flags

- Residuals stagnate while monitors drift.
- Residuals are low because equations are over-relaxed or monitors are absent.
- Long-run iteration starts before a smoke test.
- Final results are reported without conservation checks.

