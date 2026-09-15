# Workflow

The FRAME workflow provides a structured process for moving from an engineering problem to a validated implementation. It does not prescribe the same amount of work for every task. The depth of each stage should match the uncertainty, risk, and impact of the change.

The workflow consists of five stages:

1. **Foundation (F)** — Understand the problem, desired outcome, and constraints.
2. **Research (R)** — Explore viable approaches.
3. **Architecture (A)** — Choose an approach and define the implementation strategy.
4. **Materialize (M)** — Turn the strategy into a working implementation.
5. **Evaluate (E)** — Validate the result.

## Adapting the Workflow

FRAME adapts as understanding develops. Every implementation begins with Foundation and ends with Evaluate, but not every task requires Research and Architecture.

When Foundation reveals meaningful uncertainty, trade-offs, or architectural impact, the workflow enters the RAM Cycle:

`Foundation → Research → Architecture → Materialize → Evaluate`

When the problem is well understood, the implementation approach is clear and consistent with the existing system, and the change has limited risk, the workflow can use the **direct path** and skip Research and Architecture:

`Foundation → Materialize → Evaluate`

A direct path can expand into the RAM Cycle if Materialize reveals new constraints, technical uncertainty, or better alternatives. In that case, the workflow moves to Research and continues through Architecture and Materialize before Evaluate.

Foundation does not need to be repeated unless new information changes the problem, expected outcome, scope, or fundamental constraints.

Task size alone does not determine the path. A small change may still require the RAM Cycle when its impact or uncertainty is significant.

## Stages and Participants

The stages describe engineering responsibilities, not a division of labour. A single engineer or agent may carry all of them, and some may be shared — an investigation performed by someone else, or an evaluation performed by an independent reviewer — as long as the responsibilities themselves are met and one participant remains accountable for the task as a whole.

Sharing responsibilities does not change the workflow. The rules FRAME is currently trialling for delegating research and validation to separate agents are described in [Adaptive delegation](experiments/adaptive-delegation.md) and are deliberately kept out of this document.

---

## Foundation (F)

### Purpose

Foundation establishes what needs to be solved, what outcome is expected, and which context, requirements, and constraints matter.

### Key Questions

- What problem are we solving?
- What outcome do we expect, and what requirements or constraints must be respected?
- Is the implementation approach clear enough to proceed, or is Research needed next?

### Goal

A clear engineering objective and enough understanding to determine the next stage.

## Research (R)

### Purpose

Research reduces uncertainty by examining the existing system and exploring viable approaches. It should explore only as many alternatives as needed to understand the relevant trade-offs.

### Key Questions

- How does the existing system handle similar problems?
- Which approaches are technically viable?
- What are the trade-offs, risks, and unknowns?

### Goal

Enough evidence to make an informed engineering decision.

## Architecture (A)

### Purpose

Architecture turns research into an explicit engineering decision. It selects an approach, accepts its trade-offs, and defines how the solution should be implemented and integrated. The level of detail should match the scope of the task; Architecture does not require system-wide design.

### Key Questions

- Which approach should we choose, and why?
- Which trade-offs are we accepting?
- How should the solution be implemented and integrated?

### Goal

An explicit engineering decision and a clear implementation strategy.

## Materialize (M)

### Purpose

Materialize turns the chosen approach into a working implementation. If implementation reveals new constraints, invalid assumptions, or better alternatives, the workflow returns to Research.

### Key Questions

- Does the implementation follow the chosen approach and fit the existing system?
- Has the implementation revealed anything that requires the approach to be reconsidered?
- Is the result ready for evaluation?

### Goal

A working implementation ready for evaluation.

## Evaluate (E)

### Purpose

Evaluate checks whether the implementation solves the original problem, meets the relevant requirements, and fits the existing system. Its depth should match the risk and impact of the change, but the stage is never skipped.

### Key Questions

- Does the implementation solve the original problem and produce the expected outcome?
- Is the solution simple, maintainable, and well integrated?
- Has the implementation passed the relevant tests, linting, formatting, and other project checks?

### Goal

A validated solution, or a clear decision about which stage must be revisited.

If evaluation reveals a problem:

- an implementation issue returns to Materialize;
- an unsuitable approach or new technical constraint returns to Research;
- an incorrect understanding of the problem or objective returns to Foundation.

---

## RAM Cycle

Research, Architecture, and Materialize form the iterative **RAM Cycle**.

Materialize may reveal missed constraints or show that the selected approach does not work. When that happens, the workflow returns to Research, updates the decision in Architecture, and implements again.

The cycle repeats until the implementation is technically viable, then proceeds to Evaluate.
