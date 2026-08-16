# KirschQAQ

## 中国科学技术大学研究生 · 可靠 AI Agent 系统

Agent Runtime · 多智能体编排 · MCP/A2A · 恢复机制 · 可复现评测

[English](README.md)

我研究并构建在并发、中断、恢复与协议变化下仍然可理解的 AI Agent 系统，将具体故障收敛为
明确契约、持久状态与可执行的回归证据。

## 我构建的系统

| 系统 | 工程重点 | 公开证据 |
| --- | --- | --- |
| **[Pi Coding Harness](https://github.com/KirschBluteX/pi-coding-harness)** | 面向 Pi 的可选可靠性 Harness，覆盖持久化 Single/Multi 执行、崩溃恢复、不可变证据与前向 authority | [883 项测试](https://github.com/KirschBluteX/pi-coding-harness/actions/runs/31951570773) · SQLite schema 35 · Apache-2.0 |
| **[Agent Orchestration Gateway](https://github.com/KirschBluteX/agent-orchestration-gateway)** | Codex 原生 Agents 的本地控制平面，提供目的感知准入、确定性路由与有界协作写入 | 类型化 scope · 持久生命周期 receipt · 隔离并行 writer |
| **[Engineer Software](https://github.com/KirschBluteX/engineer-software)** | Codex 与 DeepSeek Harness 共享的 runtime-neutral、证据驱动软件工程工作流 | 6 种有边界工作流 · 25 个确定性路由案例 · 单一规范源 |

## 研究方向

| 方向 | 关注的问题 |
| --- | --- |
| **可靠 Agent Runtime** | 并发、取消、持久化、恢复，以及浏览器与 sandbox 生命周期 |
| **多智能体编排** | 并行执行、调度、隔离、集成 authority 与后台任务生命周期 |
| **协议互操作性** | MCP/A2A 版本兼容、任务语义、事件投递与跨 SDK 一致性 |
| **可复现评测** | 最小复现、回归测试、故障注入、benchmark 与证据边界 |

## 精选上游工程贡献

| 状态 | 项目 | 工程边界 |
| --- | --- | --- |
| **已合并** | [MudBlazor #13622](https://github.com/MudBlazor/MudBlazor/pull/13622) | 保持空表分页索引非负不变量，并补充回归覆盖 |
| **开放中** | [Microsoft Agent Framework #7679](https://github.com/microsoft/agent-framework/pull/7679) | 具有明确 .NET 工作流语义边界的声明式并行 `Foreach` 执行 |
| **开放中** | [MCP C# SDK #1814](https://github.com/modelcontextprotocol/csharp-sdk/pull/1814)、[#1815](https://github.com/modelcontextprotocol/csharp-sdk/pull/1815)、[#1816](https://github.com/modelcontextprotocol/csharp-sdk/pull/1816) | task-backed tools、MCP Apps 组合与协议版本兼容 |
| **开放中** | [A2A Go #414](https://github.com/a2aproject/a2a-go/pull/414)、[JS #659](https://github.com/a2aproject/a2a-js/pull/659)、[Python #1189](https://github.com/a2aproject/a2a-python/pull/1189) | 事件队列背压、push 版本传播与 active task 生命周期一致性 |
| **开放中** | [OpenHands SDK #4502](https://github.com/OpenHands/software-agent-sdk/pull/4502)、[#4503](https://github.com/OpenHands/software-agent-sdk/pull/4503)、[OpenHands #16614](https://github.com/OpenHands/OpenHands/pull/16614) | 浏览器可移植性、后台委派生命周期与 automation preflight 校验 |

## 研究方法

1. 明确行为契约与 authority 边界。
2. 构造能够排除薄弱解释的最小、确定性复现。
3. 跨 runtime、storage、concurrency 与 protocol 层追踪机制。
4. 将结论编码为回归或集成测试，并明确记录局限。

欢迎围绕可靠 Agent Runtime、多智能体编排、协议互操作性与可复现评测开展研究型开源协作。

仓库与上游状态核验于 2026-08-16。
