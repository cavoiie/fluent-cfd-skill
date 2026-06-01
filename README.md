# Fluent CFD Skill

[![GitHub stars](https://img.shields.io/github/stars/cavoiie/fluent-cfd-skill?style=flat&label=stars)](https://github.com/cavoiie/fluent-cfd-skill/stargazers)

<details>
<summary>简体中文</summary>

## Fluent CFD Skill

面向 Ansys Fluent、PyFluent 和 CFD 仿真工作流的 Codex skill。

这个仓库提供一个偏研究工程使用的 workflow skill，用于指导 Fluent case 设置、求解器配置、收敛诊断和 PyFluent MCP 自动化。它的定位是 agent 的判断层：不替代 Fluent 官方手册，也不打包 Fluent 运行环境。

### 亮点

- 从问题定义到结果验证的 Fluent 工作流约束。
- 面向 PyFluent MCP 的安全、可审计工具调用规范。
- 将残差、监控量、守恒检查和物理合理性结合起来判断收敛。
- 覆盖求解器选择、边界条件、湍流模型、数值格式、验证和错误恢复的参考文件。
- 面向研究使用的保守默认策略：除非本地 MCP server 显式启用，否则不执行任意 Python。

### 使用场景

- 在进入求解器前规划 Fluent case 设置。
- 检查边界条件、网格质量和物理假设。
- 选择求解器、湍流模型、近壁处理和收敛标准。
- 诊断残差停滞、出口回流、发散和启动/许可证失败。
- 指导 PyFluent MCP 工作流，例如启动 Fluent、读取 case、执行 TUI、迭代、保存和关闭会话。

### 安装

```powershell
Copy-Item -Recurse . "$env:USERPROFILE\.codex\skills\fluent-cfd"
```

</details>

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
+-- SKILL.md
+-- agents/
|   +-- openai.yaml
+-- references/
    +-- workflow.md
    +-- solver-selection.md
    +-- boundary-conditions.md
    +-- turbulence-and-wall-treatment.md
    +-- numerics-and-convergence.md
    +-- pyfluent-mcp.md
    +-- validation-checklist.md
    +-- error-recovery.md
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

## Stars

- Current stars: [GitHub stargazers](https://github.com/cavoiie/fluent-cfd-skill/stargazers)
- Trend page: [Star History](https://www.star-history.com/#cavoiie/fluent-cfd-skill&Date)
