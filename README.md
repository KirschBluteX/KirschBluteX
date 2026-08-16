# KirschQAQ

## Graduate Student at USTC · Reliable AI Agent Systems

Agent Runtimes · Multi-Agent Orchestration · MCP/A2A · Recovery · Reproducible Evaluation

[简体中文](README.zh-CN.md)

I study and build AI agent systems that remain understandable under concurrency, interruption,
recovery, and protocol change. My work turns failure modes into explicit contracts, durable state,
and executable regression evidence.

## Systems I build

| System | Engineering focus | Public evidence |
| --- | --- | --- |
| **[Pi Coding Harness](https://github.com/KirschBluteX/pi-coding-harness)** | Opt-in reliability harness for Pi with durable Single/Multi execution, crash recovery, immutable evidence, and forward-only authority | [883 tests](https://github.com/KirschBluteX/pi-coding-harness/actions/runs/31951570773) · SQLite schema 35 · Apache-2.0 |
| **[Agent Orchestration Gateway](https://github.com/KirschBluteX/agent-orchestration-gateway)** | Local control plane for Codex native Agents with purpose-aware admission, deterministic routing, and bounded cooperative writers | Typed scopes · durable lifecycle receipts · isolated parallel writers |
| **[Engineer Software](https://github.com/KirschBluteX/engineer-software)** | Runtime-neutral, evidence-driven software engineering workflow shared by Codex and DeepSeek Harness | 6 bounded workflows · 25 deterministic routing cases · one canonical source |

## Research focus

| Area | Questions I work on |
| --- | --- |
| **Reliable agent runtimes** | Concurrency, cancellation, persistence, recovery, and browser/sandbox lifecycle |
| **Multi-agent orchestration** | Parallel execution, scheduling, isolation, integration authority, and background task lifecycle |
| **Protocol interoperability** | MCP/A2A versioning, task semantics, event delivery, and cross-SDK consistency |
| **Reproducible evaluation** | Minimal reproductions, regression tests, fault injection, benchmarks, and evidence boundaries |

## Selected upstream engineering

| Status | Project | Engineering boundary |
| --- | --- | --- |
| **Merged** | [MudBlazor #13622](https://github.com/MudBlazor/MudBlazor/pull/13622) | Preserved the non-negative page-index invariant for empty tables and added regression coverage |
| **Open** | [Microsoft Agent Framework #7679](https://github.com/microsoft/agent-framework/pull/7679) | Parallel declarative `Foreach` execution with bounded .NET workflow semantics |
| **Open** | [MCP C# SDK #1814](https://github.com/modelcontextprotocol/csharp-sdk/pull/1814), [#1815](https://github.com/modelcontextprotocol/csharp-sdk/pull/1815), [#1816](https://github.com/modelcontextprotocol/csharp-sdk/pull/1816) | Task-backed tools, MCP Apps composition, and protocol-version compatibility |
| **Open** | [A2A Go #414](https://github.com/a2aproject/a2a-go/pull/414), [JS #659](https://github.com/a2aproject/a2a-js/pull/659), [Python #1189](https://github.com/a2aproject/a2a-python/pull/1189) | Event-queue backpressure, push-version propagation, and active-task lifecycle consistency |
| **Open** | [OpenHands SDK #4502](https://github.com/OpenHands/software-agent-sdk/pull/4502), [#4503](https://github.com/OpenHands/software-agent-sdk/pull/4503), [OpenHands #16614](https://github.com/OpenHands/OpenHands/pull/16614) | Browser portability, background delegation lifecycle, and automation preflight validation |

## Research practice

1. Define the behavioral contract and the authority boundary.
2. Build the smallest deterministic reproduction that can reject a weak explanation.
3. Trace the mechanism across runtime, storage, concurrency, and protocol layers.
4. Encode the result in regression or integration tests, with limitations stated explicitly.

I am open to research-oriented open-source collaboration around reliable agent runtimes,
multi-agent orchestration, protocol interoperability, and reproducible evaluation.

Repository and upstream statuses verified on 2026-08-16.
