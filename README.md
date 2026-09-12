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

## Early results

Early testing with Grok 4.6 showed FRAME using around **40% fewer reported tokens**, with a smaller implementation scope and comparable audit findings. These are initial observations from two architecture and audit comparisons, not a typical or guaranteed saving.

| Test | Without FRAME | With FRAME |
| --- | ---: | ---: |
| Action request | 933.8K | 497.1K |
| Research request | 692.1K | 413.7K |

On the action request, the FRAME run also edited two files instead of three and produced a stronger result.

## Cursor Plugin

Install FRAME in Cursor and use it on the next real change. The plugin includes:

- An **always-applied rule** that detects implementation, change, debug, and refactor work and loads the FRAME skill. It stays out of informational questions and read-only inspection. After install the rule is set to Always; you can switch it to Agent Decides or Manual in **Customize**.
- The `/frame` skill, which runs the methodology.

FRAME is markdown only. It does not open network connections, collect telemetry, or require API keys.

### Installation

**Cursor Directory.** Search for **FRAME** at [cursor.directory](https://cursor.directory) and install it from **Customize** (project or user scope).

**Local install:**

1. Clone this repository.
2. Copy the project folder to Cursor's local plugins directory as `frame`. The copy must include `.cursor-plugin/plugin.json`.

```bash
git clone https://github.com/Zicrael/FRAME.git
mkdir -p ~/.cursor/plugins/local
cp -R FRAME ~/.cursor/plugins/local/frame
```

On Windows PowerShell:

```powershell
git clone https://github.com/Zicrael/FRAME.git
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.cursor\plugins\local" | Out-Null
Copy-Item -Recurse -Force FRAME "$env:USERPROFILE\.cursor\plugins\local\frame"
```

3. Restart Cursor, or run **Developer: Reload Window**.
4. Open **Customize** and confirm the FRAME rule and the `/frame` skill are listed.

Copy the files. Do not symlink the repo into `plugins/local`: Cursor currently ignores those links.

### Usage

Ask the agent to implement or change something. With the rule set to Always, FRAME applies on its own.

- Explicit: `/frame`
- Keep it on for the session: run `/frame` with `Option+Enter` on macOS or `Alt+Enter` on Windows to use it as a Custom Mode.

### Support

Open a [GitHub Issue](https://github.com/Zicrael/FRAME/issues) for bugs, questions, or listing problems.

## Documentation

- [Principles](docs/principles.md)
- [Workflow](docs/workflow.md)
- [Changelog](CHANGELOG.md)
