# KirschQAQ

**Graduate student at USTC building reliable execution, orchestration, and evaluation
infrastructure for AI coding agents.**

Prompts determine what an agent attempts; execution, orchestration, and evaluation boundaries
determine what a team can trust after concurrent work, interruption, partial side effects, or
protocol change. I build those boundaries in my own systems and test the same design principles
through upstream work across Pi, Codex, MCP/A2A, OpenHands, Microsoft Agent Framework, and LiteLLM.

> Design rule: agent output is a proposal. Authority comes from explicit state ownership, bounded
> scope, and fresh evidence.

[简体中文](README.zh-CN.md)

### [Pi Coding Harness](https://github.com/KirschBluteX/pi-coding-harness)

**A transaction and recovery layer for Pi Coding Agent.**

I built PCH around a strict separation: models propose work; the runtime alone decides what becomes
durable. A small, passive TypeScript Bridge communicates with an on-demand Host over authenticated,
bounded RPC. SQLite WAL, immutable event chains, and content-addressed storage preserve the
Goal -> Route -> WorkCell -> Operation -> Evidence lifecycle across restarts.

A single-agent run works directly in the canonical workspace. Multi-agent runs place role-isolated
workers in credential-excluding scoped mirrors and treat every hash-bound PatchSet as an untrusted
proposal. Before serial integration can change the canonical workspace, PCH checks the lease,
fencing token, preimage, postimage, and a freshly executed oracle. After interruption, recovery
reconciles unknown side effects before authorizing exactly one next action.

**Core mechanisms:** TypeScript · authenticated HMAC RPC · SQLite WAL · immutable events · CAS ·
leases and fencing · fault injection

[Architecture](https://github.com/KirschBluteX/pi-coding-harness/blob/main/docs/ARCHITECTURE.md) ·
[Verification evidence](https://github.com/KirschBluteX/pi-coding-harness/actions/runs/31958661105)

### [Agent Orchestration Gateway](https://github.com/KirschBluteX/agent-orchestration-gateway)

**A native-agent orchestration protocol for software work.**

AOG encodes the workflow boundary I use when building with Codex Agents. Primary clarifies a software
initiative, proposes a schema-validated module DAG with non-overlapping repository scopes, and
dispatches approved modules as native Codex tasks. A bounded standard-library validator rejects
cycles, ambiguous paths, duplicate keys, and scope overlap before dispatch.

It is also practical evidence of host-level familiarity: approval, task creation, worktree isolation,
Goal/wait lifecycle, native subagents, and commit assembly are mapped onto Codex's actual primitives
instead of simulated in a parallel runtime.

The design choice is deliberate: task, worktree, Goal, wait, and native subagent are treated as
Codex-owned lifecycle primitives. AOG owns approval, dependency, write-scope, and review policy;
accepted module commits are assembled topologically on a dedicated local delivery branch. It adds
supervision and ownership rules without rebuilding a second Agent runtime or lifecycle ledger.

**Core mechanisms:** Python · stateless JSON validation · module DAGs · disjoint write scopes ·
native Codex tasks and worktrees · bounded subagents · topological commit assembly

[Workflow](https://github.com/KirschBluteX/agent-orchestration-gateway#workflow) ·
[Validator tests](https://github.com/KirschBluteX/agent-orchestration-gateway/tree/main/tests) ·
[CI evidence](https://github.com/KirschBluteX/agent-orchestration-gateway/actions/runs/31979472987)

### [Engineer Software](https://github.com/KirschBluteX/engineer-software)

**A runtime-neutral engineering decision layer for AI coding agents.**

Engineer Software keeps one canonical workflow source, exposes it as a Codex plugin, and projects it
into DeepSeek Harness's filesystem skill contract. Projection, loader, resource, and source-identity
validators turn cross-runtime drift into a failing check instead of a documentation problem.

Rather than forcing every task through a fixed pipeline, a deterministic router selects one
evidence-gated engineering mode. Routing fixtures cover activation, bypass, and legal transitions.
Paired behavior evaluations run baseline and treatment conditions in matched worktrees, preserve
raw events and patches, and report rubric scores, timing, and exact sign-test results without
turning a small pilot into a general performance claim.

**Core mechanisms:** Python · Codex plugins · DeepSeek Harness skills · generated projections ·
deterministic routing · paired behavior evaluation

[Evaluation design](https://github.com/KirschBluteX/engineer-software/blob/main/evals/README.md) ·
[Runtime compatibility](https://github.com/KirschBluteX/engineer-software/blob/main/docs/compatibility.md)

## Selected upstream engineering

### Accepted upstream

- **[MudBlazor #13622](https://github.com/MudBlazor/MudBlazor/pull/13622)** preserved the
  non-negative page-index invariant for empty tables and added regression coverage. **Merged.**

- **[Cockpit Tools #1944](https://github.com/jlcodes99/cockpit-tools/pull/1944)** hardened Linux
  Antigravity executable discovery and launch-path normalization across configured, `PATH`,
  user-local, legacy, symlink, and `bin/` layouts, with permission, metadata, and process-identity
  validation. **Merged.**

### Deeper implementations under review

**[Microsoft Agent Framework #7679](https://github.com/microsoft/agent-framework/pull/7679) -
deterministic parallel `Foreach`.** The implementation adds opt-in, bounded fan-out to declarative
.NET workflows while preserving sequential behavior by default. Each iteration runs as an isolated
sub-workflow, buffers state and events, and commits in source-index order. Failure or timeout cancels
peers and discards buffered commits. Forty focused parallel tests pass on each target framework; the
915-test unit suite passes on both `net10.0` and `net472`.

**[LiteLLM #37027](https://github.com/BerriAI/litellm/pull/37027) - bounding an OOM-prone admin
API.** I traced the failure to unbounded history reads across legacy spend-log query branches. The
change applies stable `take`/`skip` ordering everywhere, rejects invalid pagination before querying,
and preserves legacy list and summary contracts while making deprecation and pagination explicit.
The mapped endpoint suite passes 188 tests, and the current GitHub check suite is green.

**[MCP C# SDK #1816](https://github.com/modelcontextprotocol/csharp-sdk/pull/1816) - protocol
evolution without shared-state leakage.** A single typed response-emission boundary strips
unsupported fields for legacy clients, supplies defaults for current clients, and edits freshly
serialized nodes so shared result instances cannot leak state across protocol versions. Concurrent
compatibility warnings are deduplicated. The validated non-Docker scope covers 2,366 core and 617
ASP.NET Core tests.

<details>
<summary><strong>More upstream engineering</strong></summary>

- **MCP C# SDK:** [task-backed tool composition #1814](https://github.com/modelcontextprotocol/csharp-sdk/pull/1814)
  and [MCP Apps helper composition #1815](https://github.com/modelcontextprotocol/csharp-sdk/pull/1815).
- **A2A SDKs:** [subscriber backpressure in Go #414](https://github.com/a2aproject/a2a-go/pull/414),
  [wire-version propagation in JavaScript #659](https://github.com/a2aproject/a2a-js/pull/659), and
  [active-task snapshot consistency in Python #1189](https://github.com/a2aproject/a2a-python/pull/1189).
- **OpenHands:** [Windows browser discovery #4502](https://github.com/OpenHands/software-agent-sdk/pull/4502),
  [background delegation lifecycle #4503](https://github.com/OpenHands/software-agent-sdk/pull/4503),
  and [automation preflight validation #16614](https://github.com/OpenHands/OpenHands/pull/16614).
- [All authored pull requests](https://github.com/pulls?q=is%3Apr+author%3AKirschBluteX)

</details>

## Design and evaluation

- **Runtime authority:** the
  [PCH architecture](https://github.com/KirschBluteX/pi-coding-harness/blob/main/docs/ARCHITECTURE.md)
  documents process ownership, durable state, mutation authority, recovery precedence, and the
  serial integration boundary.
- **Orchestration contract:** the
  [AOG workflow and plan validator](https://github.com/KirschBluteX/agent-orchestration-gateway#plan-validation)
  define explicit approval, non-overlapping write scopes, bounded native delegation, and local
  topological assembly. Validator tests cover cycles, path safety, duplicate keys, input bounds,
  scope overlap, and deterministic normalization.
- **Workflow evaluation:** the
  [Engineer Software evaluation suite](https://github.com/KirschBluteX/engineer-software/blob/main/evals/README.md)
  combines deterministic routing contracts with matched-worktree behavior comparisons and preserves
  raw events, patches, timing, exclusions, and scoring boundaries.

## How I validate

When a unit-test boundary is narrower than the failure, I exercise the real integration path. For
[OpenHands browser discovery #4502](https://github.com/OpenHands/software-agent-sdk/pull/4502), I
combined focused selection-order regressions with the broader browser-tool suite, four real-browser
E2E cases, and an isolated Windows smoke covering the selected executable, CDP connection, DOM
state, screenshot capture, and process cleanup.

I am interested in research-oriented open-source collaboration where correctness depends on
concurrency, recovery, lifecycle, protocol, or evaluation boundaries.
