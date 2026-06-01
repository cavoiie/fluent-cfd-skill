# PyFluent MCP

Use this reference when real Fluent execution is required through the local `pyfluent` MCP server.

## Available Tools

- `server_info`: inspect MCP server status, PyFluent importability/version, active session, Ansys roots, and whether Python execution is enabled.
- `launch_fluent`: start a local Fluent session. This may consume a license.
- `connect_to_fluent`: connect to an already running Fluent server when supported.
- `session_status`: check active session and health.
- `read_case`: read a Fluent case file.
- `run_tui`: execute an explicit Fluent TUI command through the active session.
- `iterate`: run solver iterations.
- `write_case_data`: save case/data.
- `execute_python`: trusted escape hatch only when enabled by environment.
- `exit_fluent`: close the active Fluent session.

## Safe Call Order

1. `server_info`
2. Tell the user if Fluent will launch and may consume a license.
3. `launch_fluent` or `connect_to_fluent`
4. `read_case` if a case file exists.
5. `run_tui` for setup/review commands.
6. `iterate` for a short smoke run.
7. Inspect status, warnings, and relevant outputs.
8. Continue with longer runs only after the smoke run is stable.
9. `write_case_data` when state should be preserved.
10. `exit_fluent` unless the user wants to keep the session open.

## TUI Discipline

- Use explicit TUI commands and keep them auditable in the response.
- Prefer small setup changes over large opaque command batches.
- Quote paths carefully and use Fluent-friendly forward slashes when possible.
- Stop if a TUI command returns an error; do not continue a solve sequence blindly.

## `execute_python` Policy

Use `execute_python` only when:

- `server_info` shows Python execution is enabled.
- The task needs PyFluent API access that the safe tools cannot express.
- The user trusts local execution and the code is short, explicit, and reversible.

Do not use it for broad arbitrary filesystem operations or unexplained solver mutation.

## Failure Handling

- Launch failure: check Ansys root, product version, license availability, and PyFluent version.
- Missing session: call `launch_fluent` before case or TUI operations.
- Unsupported connect: use local launch or update PyFluent only when necessary.
- Tool error: summarize error, stop automation, and choose the smallest recovery.

