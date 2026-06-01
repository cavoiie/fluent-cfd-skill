# Prompt Templates

English | [简体中文](PROMPTS.zh-CN.md)

Use these templates with the `fluent-cfd` skill when asking Codex to plan, review, run, or diagnose Ansys Fluent and PyFluent CFD work.

## Full Workflow Template

```text
Use the fluent-cfd skill for this Fluent / PyFluent / CFD task.

Goal:
- [Describe the task: check convergence / set boundary conditions / choose turbulence model / run 50 PyFluent iterations]

Available files:
- Case file: [path or file name]
- Data file: [path or file name, if any]
- Mesh file: [path or file name, if any]
- Supporting material: [experiment data, screenshots, residual plots, logs]

Physics:
- Fluid: [air / water / other]
- Flow type: [internal / external / rotating machinery / multiphase / heat transfer / compressible]
- Time behavior: [steady / transient / unsure]
- Key objective quantity: [pressure drop / drag / lift / temperature / flow rate / mixing efficiency / other]
- Known boundary conditions: [inlets, outlets, walls, thermal boundaries]

Please do the following:
1. Judge whether the provided information is enough. If not, list the minimum missing information.
2. Review the setup according to the Fluent CFD workflow.
3. Explain whether the solver, physics models, turbulence model, boundary conditions, and numerics are reasonable.
4. Do not judge convergence from residuals alone. Check monitors, mass/energy conservation, and physical plausibility.
5. If PyFluent MCP is needed, state first that Fluent may launch and consume a license.
6. Run a smoke test before any long iteration sequence.
7. End with one status: runnable / numerically converged / physically credible / not trusted, with reasons.

Output format:
- Problem summary
- Key assumptions
- Review results
- Recommended changes
- PyFluent/TUI steps
- Convergence and validation criteria
- Next step
```

## Short Daily Template

```text
Use the fluent-cfd skill for this Fluent task: [task description].

Files: [case/data/log/screenshot paths]
Objective quantity: [pressure drop / force / temperature / flow rate / other]
Physics: [steady/transient, compressible/incompressible, heat transfer/multiphase/turbulent]
Boundary conditions: [inlet, outlet, wall setup]

Review this using the CFD workflow. Do not rely on residuals alone; also check monitors, conservation, and physical plausibility.
If Fluent must be launched, state that it may consume a license and run a smoke test first.
End with whether the result is trustworthy and what to do next.
```

## PyFluent MCP Run Template

```text
Use the fluent-cfd skill and pyfluent MCP for this case.

Case file:
[.cas or .cas.h5 path]

Goal:
- Launch Fluent
- Read the case
- Check session status
- Run a 20-iteration smoke test first
- If stable, run [N] more iterations
- Save case/data to: [output path]
- Close the Fluent session

Requirements:
- Before launch, state that a Fluent license/session may be consumed.
- Explain each MCP tool call.
- If divergence, reversed flow, negative volume, license failure, or TUI error appears, stop and diagnose.
- Do not use execute_python unless I explicitly allow it.
```

## Convergence Diagnosis Template

```text
Use the fluent-cfd skill to diagnose this Fluent convergence problem.

Provided information:
- Residual history: [screenshot/data]
- Monitors: [force / pressure drop / mass flow / temperature / other]
- Fluent warnings/errors: [paste log]
- Mesh quality: [skewness / orthogonal quality / y+]
- Boundary conditions: [inlets / outlets / walls]
- Model setup: [turbulence / energy / multiphase / transient]

Please determine:
1. Is this mainly a numerical issue, physics setup issue, mesh issue, or boundary-condition issue?
2. Can the current result be considered converged?
3. What is the smallest safe modification?
4. What smoke test should be run after the modification?
5. Which metrics should be used for final acceptance?
```

