# Fluent CFD Skill

[English](README.md) | [简体中文](README.zh-CN.md)

面向 Ansys Fluent、PyFluent 和 CFD 仿真工作流的 Codex skill。

这个仓库提供一个偏研究工程使用的 workflow skill，用于指导 Fluent case 设置、求解器配置、收敛诊断和 PyFluent MCP 自动化。它的定位是 agent 的判断层：不替代 Fluent 官方手册，也不打包 Fluent 运行环境。

## 亮点

- 从问题定义到结果验证的 Fluent 工作流约束。
- 面向 PyFluent MCP 的安全、可审计工具调用规范。
- 将残差、监控量、守恒检查和物理合理性结合起来判断收敛。
- 覆盖求解器选择、边界条件、湍流模型、数值格式、验证和错误恢复的参考文件。
- 面向研究使用的保守默认策略：除非本地 MCP server 显式启用，否则不执行任意 Python。

## 仓库结构

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

`SKILL.md` 保持紧凑，只负责触发、路由和核心流程；更细的判断依据按需加载 `references/` 中的文件。

## 使用场景

- 在进入求解器前规划 Fluent case 设置。
- 检查边界条件、网格质量和物理假设。
- 选择求解器、湍流模型、近壁处理和收敛标准。
- 诊断残差停滞、出口回流、发散和启动/许可证失败。
- 指导 PyFluent MCP 工作流，例如启动 Fluent、读取 case、执行 TUI、迭代、保存和关闭会话。

## 安装

将这个文件夹复制到 Codex skills 目录：

```powershell
Copy-Item -Recurse . "$env:USERPROFILE\.codex\skills\fluent-cfd"
```

安装后，当任务提到 Fluent、PyFluent、Fluent TUI、CFD 仿真设置、网格质量、边界条件、湍流模型、残差收敛、UDF 或后处理时，Codex 可以触发这个 skill。

## 安全说明

- 残差下降本身不等于收敛。
- 不应跳过网格质量、单位、边界条件一致性和近壁分辨率检查。
- 修改湍流模型必须有物理原因或验证目标。
- 除非本地工作流可信，否则应保持可选的 `execute_python` MCP 工具关闭。
- 这个仓库只包含 skill；实时控制 Fluent 需要单独的本地 PyFluent MCP server。

## 相关执行层

这个 skill 设计为配合本地 `pyfluent` MCP server 使用。该 server 可以暴露 `server_info`、`launch_fluent`、`read_case`、`run_tui`、`iterate`、`write_case_data`、`session_status` 和 `exit_fluent` 等工具。

执行层和 skill 分离，可以让本仓库保持轻量、可移植，也更适合公开发布。

## Stars

- 当前 stars：[GitHub stargazers](https://github.com/cavoiie/fluent-cfd-skill/stargazers)
- 趋势页面：[Star History](https://www.star-history.com/#cavoiie/fluent-cfd-skill&Date)
