# Error Recovery

Use this reference when Fluent fails to launch, diverges, or produces suspicious output.

## Launch or License Failure

- Run `server_info` and inspect PyFluent version, Ansys roots, and active session state.
- Check whether Fluent is installed and the version matches the PyFluent package.
- Check license availability before retrying repeated launches.
- Avoid repeatedly starting sessions; close stale sessions if possible.

## Divergence or Floating Point Exception

- Stop long iteration sequences.
- Check mesh quality, negative volumes, poor skewness, and boundary placement.
- Revisit boundary conditions, units, material properties, and operating pressure.
- Reinitialize from a physically plausible state.
- Reduce time step or under-relaxation where appropriate.
- Start with a short stable run before restoring higher-order numerics.

## Reversed Flow at Outlet

- Determine whether backflow is physical or caused by outlet placement.
- Move outlet farther downstream if recirculation crosses it.
- Define physically meaningful backflow temperature, turbulence, species, and phase values.
- Avoid relying on outflow boundaries in recirculating cases.

## Negative Volume or Mesh Failure

- Do not attempt solver fixes before fixing mesh defects.
- Inspect local cells, interfaces, dynamic mesh settings, and moving boundaries.
- Regenerate or repair the mesh if negative volumes are present.

## CFL or Transient Instability

- Reduce time step.
- Check velocity scales, mesh size, rotation speed, acoustic speed, or interface motion.
- Confirm temporal resolution matches the physics being measured.

## Residual Stagnation

- Check whether monitors are stable. Stagnation is not always failure.
- If monitors drift, review numerics, boundary conditions, mesh quality, and model stiffness.
- Check conservation balances before declaring convergence.

## Recovery Rule

Make one small, explainable change at a time, then run a short smoke test. Do not stack multiple unverified changes and then attribute success to one of them.

