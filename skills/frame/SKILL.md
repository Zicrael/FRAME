---
name: frame
description: Apply FRAME (Foundation, Research, Architecture, Materialize, Evaluate) when implementing, debugging, or refactoring software. Establish the task and existing behaviour, resolve consequential uncertainty, and validate the outcome.
---

# FRAME

Consideration before implementation.

Foundation and Evaluate apply to every engineering task. Scale the work to its risk and scope; stages do not require separate documents or narration.

- Use Foundation → Materialize → Evaluate when the outcome, affected behaviour, and approach are clear and mistakes are cheap to detect and reverse.
- Use Research → Architecture → Materialize as the RAM Cycle when uncertainty could change the approach or its correctness. Repeat only while that uncertainty remains. A direct implementation can enter RAM when new evidence requires it.

Follow-ups inherit the established context. Revisit only the outcomes, constraints, or decisions affected by new information.

Stay within the user's request. Resolve ordinary engineering decisions autonomously; involve the user for missing authority, conflicting requirements, or consequential information unavailable to you. A failed approach alone does not require escalation.

## Foundation

Establish the requested outcome and explicit constraints before changing code. If the requested change would not achieve that outcome, explain the mismatch before implementing.

Read the affected code, its callers, and relevant tests or documentation. Work from the code, not from filenames or recollection. Trace shared values and contracts where evidence indicates other consumers. Stop expanding the investigation once the affected behaviour and credible impact are understood.

Identify behaviour and contracts that must survive, including those the prompt omits. Distinguish intended behaviour from defects and incidental implementation choices; preserving behaviour does not require preserving internal structure. Name the evidence that would demonstrate the requested outcome and the check most likely to expose a consequential regression; the direct path needs both as much as RAM does.

For broad improvement requests, choose a bounded outcome supported by concrete findings. Separate necessary changes from optional improvements and issues to report. Finding an issue does not automatically authorise fixing it.

Choose the direct path or RAM based on unresolved questions and risk. Concrete reasons to enter RAM include an unexplained failure, competing approaches with materially different consequences, unverified dependency or API behaviour, or uncertain effects on callers, data, performance, concurrency, or security. Identify the question that needs resolving. Crossing files or module boundaries alone does not require RAM; a one-line change can require it.

## Research

Resolve the questions that prevent a sound implementation decision.

- Start with relevant existing patterns. Compare alternatives only when their trade-offs could change the decision; no fixed number is required.
- Verify assumptions the approach depends on using code, focused experiments, or authoritative documentation for the relevant version. Existing usage does not prove a proposed variation is supported.
- For defects, establish a cause supported by a reproduction, code, logs, or traces. When reproduction is unavailable, identify the evidence and remaining uncertainty rather than treating a guess as a diagnosis.

Each further investigation should answer a question that could change the decision. Stop when the evidence supports an approach; unknowns that can be checked during Evaluate need not delay implementation.

## Architecture

Choose an approach consistent with the evidence and task constraints. Explain consequential choices and their trade-offs so the engineer can assess them. Identify the changes and integration points. Find the most consequential ways it could fail and the smallest practical checks that would expose them.

Keep this proportional: a local decision can be brief. An invalidated approach returns to Research; ask the user only when the remaining options require authority or information you do not have.

## Materialize

Implement the simplest solution that meets the established outcome and contracts, following project conventions. Cover the input domain the contract admits, not just the examples in the prompt. Avoid unrelated cleanup and speculative capabilities.

Preserve required behaviour while simplifying internal structure where useful. If implementation disproves an assumption or reveals an unsuitable approach, return to Research instead of stacking workarounds. Return to Foundation if the problem or intended outcome itself changes.

Read [references/ram-cycle.md](references/ram-cycle.md) when the cycle repeats or an Architecture decision must be replaced. Carry forward evidence and rejection reasons rather than restarting the investigation.

## Evaluate

Evaluate against the original outcome and constraints, prioritising risks introduced by the change.

1. Exercise changed behaviour and affected contracts through their consumers. Check relevant integration, intermediate, boundary, and failure states. For presentation changes, inspect the rendered result when possible.
2. Use existing meaningful tests and add regression coverage where needed. Verify expected results independently when shared implementation logic could conceal a defect. For failures that cannot be reproduced reliably, test the changed mechanism. Use direct verification when automated tests are impractical or merely repeat implementation details, and report remaining gaps.
3. Run relevant project checks using commands from the repository or CI: tests, type checking, linting, and build as applicable. Distinguish introduced failures from existing or environmental ones; report blocked checks without absorbing unrelated repairs.
4. Inspect the diff for unintended behaviour changes, unnecessary scope, dead code, and unhandled failures. If tests were removed or weakened, preserve the useful coverage they provided. Check that required preserved behaviour has coverage or explicitly identify the gap.

A fallback must meet its contract or expose failure. An interrupted or incomplete check does not establish success. Diff review and passing tests prove only what they cover; name material behaviour that remains unverified.

Fix implementation defects in Materialize, reconsider unsuitable approaches in Research, and revisit misunderstood outcomes in Foundation. Once the outcome and relevant checks are satisfied, stop; further investigation needs a concrete unresolved risk or required check.

## Delegation (experimental)

One lead owns the task throughout: it maintains Foundation, selects the approach, writes the implementation, resolves reported findings, and reports completion. A delegated agent carries out the responsibility it was assigned; it does not restart FRAME.

Start with one agent, then consider the two extensions separately. Delegate research when a bounded, decision-relevant question benefits from separate context, specialised investigation, or exploration genuinely separable from the implementation; keep the investigation yourself when you can resolve the question directly for less expected work than delegating it. Add independent validation when a consequential behaviour remains weakly verified, or when verification rests on assumptions a separate assessment could meaningfully challenge. Task size, file count, uncertainty alone, or confidence alone do not decide how many agents work on a task, and an important task alone is not an assignment.

Read [references/delegation.md](references/delegation.md) before the first delegation. Where delegation is unavailable or not permitted, continue as a single agent and report the verification actually performed.

## Communication

Keep routine process internal. Explain consequential decisions, trade-offs, changed assumptions, and blockers when they matter to the user. Finish with the result, relevant checks, and material limitations. Do not mechanically narrate FRAME stages.
