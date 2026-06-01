# Solver Selection

Use this reference when choosing Fluent solver settings or reviewing whether a case setup matches the physics.

## Primary Choices

- Pressure-based solver: default for most incompressible, low-speed, and mildly compressible flows.
- Density-based solver: prefer for high-speed compressible flows with shocks, strong wave behavior, or tightly coupled density-pressure dynamics.
- Steady: use only when boundary conditions and expected flow features are time-independent and the target quantity should settle.
- Transient: use for vortex shedding, rotating/moving geometry with time-resolved effects, startup/shutdown, sloshing, unsteady multiphase, or any objective depending on time history.

## Physics Toggles

- Energy equation: enable for heat transfer, buoyancy with temperature variation, compressible flow, conjugate heat transfer, radiation, or temperature-dependent properties.
- Gravity: enable for buoyancy, free-surface orientation, settling, hydrostatics, or density-stratified flow.
- Multiphase: require phase inventory, interface/dispersion assumption, phase interaction model, and expected observable before choosing VOF, mixture, Eulerian, or DPM.
- Rotating machinery: distinguish frame change from physical motion. Use MRF for steady approximate rotating regions; use sliding mesh for time-resolved blade-passing or transient interaction.

## Questions To Resolve

- What is the Mach number or expected compressibility effect?
- Is the goal a time-average, final steady value, or transient waveform?
- Is separation, swirl, shock, phase interface, heat transfer, or chemical reaction central to the result?
- Are reference values and operating pressure physically meaningful for the expected outputs?

## Guardrails

- Do not select a more complex model just because it is available.
- Do not use steady MRF when the user's target is inherently unsteady.
- Do not ignore density/temperature coupling when buoyancy or compressibility drives the flow.

