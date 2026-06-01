# Boundary Conditions

Use this reference for Fluent boundary setup and review.

## General Checks

- Confirm all zone names and types match the physical geometry.
- Check units for every scalar: velocity, pressure, mass flow, temperature, turbulence intensity, hydraulic diameter, and heat flux.
- Ensure inlet/outlet choices match what is actually known. Do not impose both flow rate and pressure drop unless the model requires it.
- Confirm reference/operating pressure conventions before interpreting gauge pressures.
- Check whether outlet backflow conditions are physically defined for temperature, turbulence, and phase variables.

## Common Boundaries

- Velocity inlet: use when direction and velocity profile are known. Provide turbulence quantities and temperature/species/phase data if active.
- Mass-flow inlet: use when total inflow rate is known and density handling is appropriate.
- Pressure inlet: use for compressible or open-domain cases when total/static pressure and flow direction assumptions are known.
- Pressure outlet: common outlet when downstream static pressure is known or acceptable. Watch reversed flow warnings.
- Outflow: use cautiously; avoid where backflow, strong gradients, or recirculation may cross the outlet.
- Wall: check no-slip/slip, roughness, heat flux/temperature/conjugate coupling, wall motion, and wall treatment compatibility.
- Symmetry: use only where normal velocity and normal gradients are physically zero.
- Periodic: require matching topology and a valid periodic pressure/mass-flow assumption.
- Interface: confirm conformal/non-conformal pairing and whether mesh interfaces or sliding interfaces are intended.

## Rotating and Moving Zones

- For MRF, define rotating cell zones and stationary/rotating interfaces consistently.
- For sliding mesh, verify time step, interface pairing, and transient objective.
- For moving walls, distinguish wall motion from rotating frame motion.

## Red Flags

- Outlet placed inside a recirculation region.
- Inlet turbulence values left as meaningless defaults.
- Wall thermal condition omitted in a heat-transfer case.
- Symmetry used as a convenience instead of a physical symmetry plane.
- Gauge pressure interpreted without checking operating pressure.

