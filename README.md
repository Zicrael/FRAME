<p align="center">
  <picture>
    <source
      media="(prefers-color-scheme: dark)"
      srcset="./assets/header-dark.svg"
    >
    <source
      media="(prefers-color-scheme: light)"
      srcset="./assets/header-light.svg"
    >
    <img
      src="./assets/header-light.svg"
      alt="FRAME"
      width="850"
    >
  </picture>
</p>

AI agents can write code quickly. FRAME helps engineers and agents decide what to build, understand why, and check that it solves the problem.

FRAME is a lightweight engineering methodology for moving from a problem to a validated implementation. Understand the existing system, investigate meaningful uncertainty, choose an approach, and reconsider it when new evidence changes the picture. The goal is to avoid premature implementation and repeated fixes built on the wrong assumption.

The methodology is independent of any AI model, development tool, programming language, or implementation framework. AI assists throughout the process; engineers remain responsible for the decisions.

## Core Philosophy

At the heart of FRAME is a simple idea:

> **Consideration before Implementation.**

## How FRAME Works

FRAME consists of five stages, with each letter representing a distinct part of the engineering process:

1. **Foundation** — Understand the problem, desired outcome, and constraints.
2. **Research** — Explore viable approaches.
3. **Architecture** — Choose an approach and define the implementation strategy.
4. **Materialize** — Turn the strategy into a working implementation.
5. **Evaluate** — Validate the result.

Clear, low-risk tasks take the direct path: **Foundation → Materialize → Evaluate**. When meaningful uncertainty remains, Research, Architecture, and Materialize form the iterative **RAM Cycle**. A direct implementation can enter that cycle if it reveals unexpected complexity. Evaluate always happens; its depth matches the task.

FRAME contains only instructions and plugin metadata. The plugin itself runs no scripts or hooks, collects no telemetry, and requires no additional credentials.

## Research and Validation Helpers

FRAME runs as one agent by default. Where the host supports subagents, that agent can optionally call on two helpers:

- a **researcher**, for a bounded question whose answer could change the implementation decision;
- a **validator**, which assesses a candidate change against the original requirements and the behaviour that had to be preserved, without having written it.

One lead agent always owns the task: it establishes Foundation, chooses the approach, writes the code, resolves reported findings, and reports the result. Helpers carry out the responsibility they were assigned, write no production code, and do not delegate further. Where subagents are unavailable or disabled, FRAME runs as a single agent and reports the verification it actually performed.

Adaptive delegation is **experimental**. Its routing criteria, and the measurements intended to establish whether it is worth its cost, are described in [Adaptive delegation](docs/experiments/adaptive-delegation.md). Those measurements have not been carried out yet, so FRAME makes no claim that delegation improves quality, speed, or cost.

## Case Studies

Each case study runs the same engineering task twice on a real codebase: once with FRAME and once without it. Both runs use the same model, prompt, and starting code.

| Case study | Without FRAME | With FRAME | Difference | Review result |
| --- | ---: | ---: | ---: | --- |
| [Sudoku generator](docs/case-studies/sudoku-generator.md) | 4.5M tokens | 3.5M tokens | 22% fewer | FRAME preferred for largely retaining rotational symmetry |

## Installation

Install FRAME as a plugin in Claude Code or Cursor.

### Claude Code

```text
/plugin marketplace add Zicrael/FRAME
/plugin install frame@frame
```

Run each command separately.

In the Claude desktop app, open the **Code** tab and enter the same commands in the prompt box.

Ask Claude to implement or change something. Claude can load FRAME automatically when the request matches the skill description. Explicit invocation is `/frame:frame`.

### Cursor

Install FRAME in Cursor and use it on the next real change. The plugin includes:

- An **always-applied rule** that detects implementation, change, debug, and refactor work and loads the FRAME skill. It stays out of informational questions and read-only inspection. After install the rule is set to Always; you can switch it to Agent Decides or Manual in **Customize**.
- The `/frame` skill, which runs the methodology.
- Two optional agents, `frame-researcher` and `frame-validator`, which the skill uses only when its routing criteria are met.

Ask the agent to implement or change something. With the rule set to Always, FRAME applies on its own. Explicit: `/frame`. To keep it on for the session, run `/frame` with `Option+Enter` on macOS or `Alt+Enter` on Windows to use it as a Custom Mode.

### Full plugin (recommended)

Install FRAME as a local Cursor Plugin.

**macOS / Linux**

```bash
mkdir -p ~/.cursor/plugins/local
git clone https://github.com/Zicrael/FRAME.git ~/.cursor/plugins/local/frame
```

**Windows PowerShell**

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.cursor\plugins\local" | Out-Null
git clone https://github.com/Zicrael/FRAME.git "$env:USERPROFILE\.cursor\plugins\local\frame"
```

Restart Cursor or run **Developer: Reload Window**, then open **Customize → Plugins** and confirm that FRAME contains the rule, the `frame` skill, and the two agents.

> For Teams and Enterprise, local plugin imports can be disabled by an administrator.

### If local plugins are disabled

Install FRAME directly into the project instead:

```text
rules/*.mdc       → .cursor/rules/
skills/frame/     → .cursor/skills/frame/
agents/*.md       → .cursor/agents/
```

Cursor automatically discovers project rules, skills, and agents from these directories. Omit `agents/` to run FRAME as a single agent. Commit them if you want FRAME to be shared with the repository, or add .cursor/ to .gitignore to keep the installation local.

### Cursor Directory

FRAME is also listed on [Cursor Directory](https://cursor.directory/plugins/frame).

Cursor Directory currently installs the FRAME rule only. For the complete plugin with the `frame` skill, use the local plugin installation above.

## Support

Open a [GitHub Issue](https://github.com/Zicrael/FRAME/issues) for bugs, questions, or listing problems.

## Documentation

- [Principles](docs/principles.md)
- [Workflow](docs/workflow.md)
- [Adaptive delegation (experimental)](docs/experiments/adaptive-delegation.md)
- [Changelog](CHANGELOG.md)
