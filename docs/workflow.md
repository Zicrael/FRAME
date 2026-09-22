# Workflow

FRAME moves an engineering request to a result its evidence supports. It does not prescribe the same amount of work for every task.

> FRAME guides engineering judgment. The requested outcome determines the work; uncertainty and verification needs determine the effort and the participants.

FRAME names five responsibilities:

1. **Foundation (F)** — Understand the requested outcome, constraints, and relevant existing behaviour.
2. **Research (R)** — Resolve the uncertainty that could change the solution.
3. **Align (A)** — Assess the approach against the real implementation context and decide how to proceed.
4. **Materialize (M)** — Carry out the authorised implementation.
5. **Evaluate (E)** — Assess whether the deliverable satisfies the original request.

They are responsibilities, not a schedule. Meeting them does not require five separate conversations, five documents, or five rigidly ordered passes.

## Scaling the Work

Foundation and Evaluate apply to every task. Research and Align can each be brief when the approach is already clear, and substantial when it is not.

| Request | What completing it means |
| --- | --- |
| A straightforward change | Understand it, implement it, verify it. |
| A question, diagnosis, or comparison | Findings with their evidence, and a recommendation where the evidence supports one. No code is owed. |
| Diagnosis followed by a fix | An established cause, then the implementation and its checks. |
| A broad improvement request | Enough investigation and implementation to reach the outcome it asks for. |

Two things follow from this. The first is that effort is earned rather than assumed: a request to fix something does not by itself call for deep research, and task size alone does not decide how much investigation a change needs. A one-line change can require a real investigation, and a change spanning several files can be obvious.

The second is that the initial plan stays revisable. When evidence shows that reaching the requested outcome needs related work — a consumer the change breaks, a contract it violates, a defect the fix exposes — that work belongs to the task. Genuinely optional improvements stay separate from what completion requires. The requested outcome itself holds unless the user changes it; understanding and solutions may be corrected, requirements may not be quietly weakened so that a result can pass.

## Iteration

FRAME does not need a separate named cycle to iterate. Any responsibility can be revisited when evidence calls for it, and the useful discipline is in how that revisiting happens:

- when an attempt fails, investigate the failure before replacing the approach, so the next attempt is not aimed at a misdiagnosed cause;
- carry established evidence forward instead of restarting the investigation;
- keep the reason each rejected alternative was rejected. It comes back into scope when that reason no longer holds; difficulty alone does not remove it;
- before another attempt, name the question it would answer.

## Responsibilities and Participants

The five responsibilities describe engineering work, not a division of labour. One engineer or agent may carry all of them. Some may be shared — an investigation performed by someone else, an assessment performed by an independent reviewer — as long as the responsibilities are met and one participant remains accountable for the task as a whole.

Whether to share them is a judgment about uncertainty, consequences, the value of an independent check, and whether the work separates usefully. That judgment is deliberately kept out of this document: [Delegation](delegation.md) covers the arrangements FRAME supports, how to choose one, and how a helper's findings come back, and the operational instructions agents follow during a handoff are in [`skills/frame/references/delegation.md`](../skills/frame/references/delegation.md).

---

## Foundation (F)

### Purpose

Foundation establishes the outcome being requested, the constraints that bear on it, and the existing behaviour it touches. It locates the code, consumers, tests, and documentation the task actually depends on, and works from those sources rather than from recollection.

### Key Questions

- What outcome is being requested, and what constraints must be respected?
- Which behaviour and contracts have to survive the change, including those the request does not mention?
- Would the change as requested actually achieve the outcome as requested?
- Is the approach clear enough to proceed, or does something need resolving first?

### Goal

A clear engineering objective and enough understanding of the system to decide what the task requires.

## Research (R)

### Purpose

Research resolves the uncertainty that could change the solution: the cause of a defect, how a dependency actually behaves, the consequences for consumers, or the difference between candidate approaches. It produces usable evidence rather than reassurance. Where findings are the deliverable, Research is the substance of the task.

### Key Questions

- What is the established cause, and what evidence supports it?
- Which assumptions does the approach depend on, and have they been verified against the code, an experiment, or authoritative documentation for the version in use?
- Where do the alternatives differ in a way that would change the decision?
- What remains uncertain, and does that uncertainty still affect the solution?

### Goal

Evidence sufficient to decide on, with its sources, its remaining uncertainty, and a recommendation where one is warranted.

## Align (A)

### Purpose

Align turns understanding into a decision. It tests the proposed approach against the implementation context actually found, accepts the trade-offs, and identifies the changes and integration points. Where research was delegated, Align examines its evidence and the consequential assumptions rather than adopting a summary.

Align is an engineering decision, not a mandatory approval gate. Its depth matches the scope of the task; it does not require system-wide design.

### Key Questions

- Which approach are we taking, and which trade-offs does it accept?
- Does the evidence behind it hold up against the sources?
- How should the solution be implemented and integrated?
- Does anything here need authority or information we do not have?

### Goal

An explicit decision, and a clear enough implementation strategy to act on.

## Materialize (M)

### Purpose

Materialize carries out the authorised implementation: the simplest solution that satisfies the established outcome and contracts, following the project's conventions. It includes the related work the outcome requires and leaves out unrelated cleanup and speculative capability. If implementation disproves an assumption or shows the approach is unsuitable, the investigation and the decision are revisited instead of accumulating workarounds.

### Key Questions

- Does the implementation satisfy the outcome and cover the input domain the contract admits?
- Is required behaviour preserved, while the defects in scope are corrected?
- Has implementation revealed anything that changes the decision?

### Goal

A candidate worth evaluating.

## Evaluate (E)

### Purpose

Evaluate assesses whether the deliverable satisfies the original request, including required work that may have been omitted rather than only behaviour that broke. The evidence it uses fits the task: tests and project checks, execution through real consumers, source inspection, the rendered result, or authoritative sources for a research deliverable.

### Key Questions

- Does the deliverable satisfy the original request, and is any required work missing?
- Is the behaviour that had to survive still intact, at boundary and failure states as well as the common path?
- Were expected results established independently of the implementation's own logic?
- What remains unverified, and which checks were blocked?

### Goal

A result its evidence supports, or a clear account of what has to be corrected.

## Correction

Evaluation results re-enter the work where their cause lies, and only what needs resolving goes back:

| Result | Next action |
| --- | --- |
| Implementation defect, or required work omitted | Repair it and recheck the behaviour affected. |
| Invalid assumption or unsuitable approach | Revisit the relevant investigation and the decision built on it. |
| The requested outcome was misunderstood | Correct the understanding against the original request. |
| Missing evidence | Run the smallest practical check that resolves the uncertainty. |
| A finding the evidence does not support | Weigh that evidence before changing anything. |
| An optional improvement | Keep it out of what completion requires. |

Completion means the request is satisfied and the evidence supports it. A required defect that was reported and left unrepaired is not complete, and a residual-issues list is not a repair. Where progress depends on information or authority no participant has, the concrete blocker is the result to report.
