---
name: fluent-cfd
description: Guide Ansys Fluent and PyFluent CFD simulation workflows with MCP tool-use discipline. Use when Codex works on Fluent, PyFluent, Fluent TUI, CFD or fluid simulation setup, case/data files, mesh quality, boundary conditions, turbulence models, residual convergence, UDFs, post-processing, solver diagnostics, or validation of Ansys Fluent results.
---

# Fluent CFD

Use this skill as the workflow and judgment layer for Ansys Fluent work. Keep Fluent documentation as the fact source, use the local `pyfluent` MCP server as the execution layer, and use this skill to decide the order of operations, checks, and validation criteria.

## Operating Rules

- Define the physics before touching the solver: objective quantity, geometry, units, fluid, regime, steady/transient behavior, compressibility, heat transfer, multiphase, rotating zones, and expected validation evidence.
- Do not treat residual decrease alone as convergence. Require monitor stabilization and conservation checks for the quantities that matter.
- Do not skip mesh quality, units, boundary-zone naming, boundary-condition consistency, and wall-resolution checks.
- Do not change turbulence models without a physical reason or a stated validation purpose.
- Prefer safe MCP tools and explicit Fluent TUI commands. Use `execute_python` only when `PYFLUENT_MCP_ENABLE_PYTHON=1` and the workflow is trusted.
- Before starting Fluent or consuming a license, state that the action will launch Fluent and may occupy a license/session.
- End live Fluent sessions with `exit_fluent` when the task is complete unless the user asks to keep the session open.

## Workflow

1. Frame the case: identify objective metrics, physics, known inputs, missing data, expected outputs, and acceptance criteria.
2. Choose solver and models: decide pressure-based vs density-based, steady vs transient, energy, multiphase, turbulence, wall treatment, and reference values.
3. Check the mesh and setup basis: units, cell/face zones, boundary names, quality metrics, non-orthogonality/skewness, and y+ target.
4. Set or review materials, boundary conditions, operating/reference conditions, numerics, initialization, and monitors.
5. Run a smoke test first: a short iteration/time-step run to catch setup errors before a full solve.
6. Iterate or advance time while monitoring residuals, integral balances, and objective quantities.
7. Save case/data and report validation status, remaining risks, and next checks.

## Reference Loading

Load only the reference files needed for the current task:

- `references/workflow.md`: complete Fluent workflow and task routing.
- `references/solver-selection.md`: model and solver selection rules.
- `references/boundary-conditions.md`: inlet, outlet, wall, symmetry, periodic, and rotating-zone boundary checks.
- `references/turbulence-and-wall-treatment.md`: turbulence model, wall treatment, y+, and mesh implications.
- `references/numerics-and-convergence.md`: discretization, initialization, monitors, residuals, and convergence.
- `references/pyfluent-mcp.md`: local `pyfluent` MCP tools, call order, safety limits, and failure handling.
- `references/validation-checklist.md`: conservation, mesh independence, physical plausibility, and post-processing checks.
- `references/error-recovery.md`: divergence, reversed flow, negative volume, CFL, residual stalls, and launch/license failures.

## MCP Tool Discipline

When a task requires real Fluent execution through the local MCP server:

1. Call `server_info` first to confirm PyFluent, Ansys roots, and whether Python execution is enabled.
2. Call `launch_fluent` only after stating that Fluent will start and may consume a license.
3. Use `read_case` for existing `.cas`, `.cas.h5`, or equivalent case files.
4. Use `run_tui` for explicit, auditable Fluent TUI commands.
5. Use `iterate` for a defined iteration count; prefer a short smoke run before long runs.
6. Use `session_status` after suspicious behavior or long operations.
7. Use `write_case_data` before closing if the state should be preserved.
8. Use `exit_fluent` at the end of the workflow unless the user explicitly wants the session left open.

If a tool returns an error, stop the automation sequence, summarize the failure, read `references/error-recovery.md` if relevant, and propose the smallest safe recovery.

