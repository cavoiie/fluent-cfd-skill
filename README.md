# Fluent CFD Skill

A Codex skill for Ansys Fluent, PyFluent, and CFD simulation workflows.

This repository packages a research-oriented workflow skill for working with Fluent cases, solver setup, convergence diagnosis, and PyFluent MCP automation. It is designed as a judgment layer for agents: it does not replace the Fluent manuals, and it does not bundle a Fluent runtime.

## Highlights

- Fluent workflow discipline from problem framing to validation.
- PyFluent MCP tool-use guidance for safe, auditable Fluent automation.
- Convergence checks that combine residuals, monitors, conservation, and physical plausibility.
- Practical references for solver choice, boundary conditions, turbulence, numerics, validation, and error recovery.
- Conservative defaults for research use: no arbitrary Python execution unless explicitly enabled in the local MCP server.

## Repository Layout

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── workflow.md
    ├── solver-selection.md
    ├── boundary-conditions.md
    ├── turbulence-and-wall-treatment.md
    ├── numerics-and-convergence.md
    ├── pyfluent-mcp.md
    ├── validation-checklist.md
    └── error-recovery.md
```

`SKILL.md` is intentionally compact. It routes the agent through the core CFD workflow and points to focused references only when needed.

## Use Cases

- Plan a Fluent case setup before touching the solver.
- Review boundary conditions, mesh quality, and physical assumptions.
- Choose solver settings, turbulence models, wall treatment, and convergence criteria.
- Diagnose residual stalls, reversed flow, divergence, and launch/license failures.
- Guide PyFluent MCP workflows such as launch, read case, run TUI commands, iterate, save, and close.

## Installation

Copy this folder to your Codex skills directory:

```powershell
Copy-Item -Recurse . "$env:USERPROFILE\.codex\skills\fluent-cfd"
```

After installation, Codex can trigger the skill when a task mentions Fluent, PyFluent, Fluent TUI, CFD simulation setup, mesh quality, boundary conditions, turbulence models, residual convergence, UDFs, or post-processing.

## Safety Notes

- Residual decrease alone is not convergence.
- Mesh quality, units, boundary consistency, and wall-resolution checks should not be skipped.
- Turbulence model changes should have a physical reason or validation goal.
- The optional `execute_python` MCP tool should stay disabled unless the local workflow is trusted.
- This repository contains only the skill. A separate local PyFluent MCP server is required for live Fluent control.

## Related Execution Layer

The skill is designed to pair with a local `pyfluent` MCP server that exposes tools such as `server_info`, `launch_fluent`, `read_case`, `run_tui`, `iterate`, `write_case_data`, `session_status`, and `exit_fluent`.

That execution layer is intentionally separate from this repository so this skill remains lightweight, portable, and safe to publish.

