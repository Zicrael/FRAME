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

AI agents can write code quickly. FRAME helps engineers and agents turn engineering requests into results supported by evidence.

FRAME is a lightweight engineering methodology that scales investigation, implementation, and validation to the task. Understand the requested outcome and the existing system, resolve uncertainty that could change the approach, and check the result against the requirements. One agent can carry the work; research or validation helpers join when their contribution justifies the additional effort. The goal is to reduce avoidable mistakes and repeated rework on the way to a verified result.

FRAME is independent of any AI model, development tool, programming language, or implementation framework. Agents make engineering decisions within the authority granted by the task. Engineers retain control over goals, constraints, and acceptable trade-offs.

## Core Philosophy

At the heart of FRAME is a simple idea:

> **Consideration before Implementation.**

FRAME guides engineering judgment. The requested outcome determines the work; uncertainty and verification needs determine the effort and the participants.

## How FRAME Works

FRAME names five engineering responsibilities:

1. **Foundation** — Understand the requested outcome, constraints, and relevant existing behaviour.
2. **Research** — Resolve the uncertainty that could change the solution.
3. **Align** — Assess the approach against the real implementation context and decide how to proceed.
4. **Materialize** — Carry out the authorised implementation.
5. **Evaluate** — Assess whether the deliverable satisfies the original request.

They are responsibilities rather than a fixed sequence of meetings or documents. Every task needs Foundation and Evaluate. A straightforward change can move from understanding to implementation and verification, with Research and Align taking a sentence each. A request for findings finishes at Evaluate with supported findings and no code. Work grows because a question is unresolved or a consequence is unverified, not because a task sounds serious — and the plan stays revisable when evidence shows the outcome needs related work.

FRAME contains only instructions and plugin metadata. The plugin itself runs no scripts or hooks, collects no telemetry, and requires no additional credentials.

## Research and Validation Helpers

FRAME starts with one accountable lead carrying all five responsibilities. Where the host supports subagents, that lead can add a helper when the helper has a concrete contribution to make:

- a **researcher**, when a substantial investigation benefits from its own context;
- a **validator**, when a separate assessment could expose consequential mistakes, omissions, or unsupported assumptions.

The two are independent choices: delegating the investigation does not commit the lead to delegating the assessment. The lead keeps the original request, decides the approach, writes the code, resolves reported findings, and remains accountable for completion. Helpers carry out the responsibility they were assigned, write no production code, and do not delegate further. Where subagents are unavailable or disabled, FRAME runs as a single agent and reports the verification it actually performed.

Adaptive delegation is a supported capability: one agent is the default, the arrangement is chosen per task, and no task requires a helper. FRAME makes no claim that delegation improves quality, speed, or cost. [Delegation](docs/delegation.md) describes the arrangements, how one is chosen, and how a helper's findings return to the lead.

## Case Studies

These case studies compare FRAME with unguided implementations on real codebases, documenting outcomes, token usage, and review findings. Each study describes its setup and limitations.

| Case study | FRAME version | Without FRAME | With FRAME | Review result |
| --- | --- | ---: | ---: | --- |
| [Sudoku generator](docs/case-studies/sudoku-generator.md) | v1.1 | 4.5M tokens | 3.5M tokens | FRAME preferred for better preservation of rotational symmetry |
| [Racing game](docs/case-studies/racing-game.md) | v2.0 | 4M tokens | 5.6M tokens | FRAME preferred for usability, reliability, and visual consistency |

These are individual observations, not estimates of FRAME’s typical quality or cost. Comparisons should be read alongside the setup and limitations in each study.

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

- An **always-applied rule** that detects implementation, change, debug, and refactor work — and investigation where the answer has to be established from the system rather than recalled — then loads the FRAME skill. It stays out of explaining existing code and simple lookup. After install the rule is set to Always; you can switch it to Agent Decides or Manual in **Customize**.
- The `/frame` skill, which runs the methodology.
- Two optional agents, `frame-researcher` and `frame-validator`, which the lead uses only when a helper has a concrete contribution to make.

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
- [Delegation](docs/delegation.md)
- [Changelog](CHANGELOG.md)
