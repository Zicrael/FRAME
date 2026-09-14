---
name: frame
description: Applies the FRAME engineering methodology (Foundation, Research, Architecture, Materialize, Evaluate) to software-engineering work. Use when implementing, changing, extending, debugging, or refactoring code, to establish the problem and the existing system before implementing and to validate the result against the original problem afterwards.
---

# FRAME

Consideration before implementation.

Foundation and Evaluate happen on every task. Research and Architecture happen only while meaningful uncertainty remains.

- Direct path: Foundation, Materialize, Evaluate.
- RAM Cycle: Foundation, then Research, Architecture and Materialize repeating while uncertainty remains, then Evaluate.

Each stage's depth scales with the risk and scope of the change. The steps below state what has to be true before moving on; they are not a script to perform or narrate. On a contained change, Foundation is a minute of reading. On a new subsystem it is real work.

Follow-ups inherit Foundation. Incorporate the new constraints and evidence, and reconsider the decisions they affect. Revisit Foundation when the objective, expected outcome, or task boundary changes.

If the user asks for less process, reduce the depth and the reporting, not the path. When something below still calls for the RAM Cycle, say which concern in one sentence and carry on. Evaluate happens either way.

FRAME does not grant permission to implement beyond the user's request.

Involve the user when a decision needs authority they have not given, when their stated requirements cannot be satisfied together, or when progress depends on information only they have. A failed approach, a disproved assumption, or an incomplete diagnosis is a reason to investigate further, not a reason to stop.

## Foundation

Do this before touching code, on every task.

1. Restate the problem to yourself in terms of the system rather than the request.
2. Establish the expected outcome: what is true after the change that is not true now.
3. Read the code the change touches, how it is called, and what depends on it. Work from the code, not from filenames or recollection.
4. Find the other places the same value, behaviour, or decision is expressed. Duplicated constants, parallel implementations, and published contracts are what make a change larger than it looks.
5. Identify the existing behaviour and contracts that must survive the change, including those absent from the request. Use code, callers, documentation, and tests as evidence; distinguish intended behaviour from defects and incidental implementation choices.

Enough has been read once the affected contracts and the credible impact are established. Follow a further dependency when evidence points at it, not to complete a survey of the repository.

Treat every explicit user constraint as an acceptance criterion. If constraints conflict, explain the conflict and ask which one to relax. Do not invent unsupported compatibility.

Resolve factual questions from available evidence. Ask the user when ambiguity changes the implementation or a conflict requires their decision.

If the change as requested would not solve the problem behind it, say so before implementing rather than afterwards.

### Choosing the path

Take the direct path only when all of these hold:

- the expected outcome is unambiguous;
- one implementation is apparent, consistent with the existing system, and supported by evidence for the behaviour it changes or promises to preserve;
- the affected surface is known, and Foundation found nothing that extends it;
- the consequences of being wrong would be cheap to detect and reverse.

Otherwise run the RAM Cycle. Common triggers: several plausible designs with materially different consequences; a new dependency, data model, interface, or migration; a change that crosses module boundaries or alters existing callers; an unexplained defect; performance, concurrency, or security behaviour that cannot be predicted by reading; an unfamiliar library whose behaviour would otherwise be guessed.

Size is not the criterion. A one-line change inside a widely used function can need the RAM Cycle, and a large amount of obvious mechanical work may not.

## Research

Goal: enough evidence to decide. Not a survey.

1. Find how the existing system already handles this class of problem. Follow that precedent unless there is a reason not to.
2. Compare alternatives only while more than one approach remains plausible. Do not generate alternatives to fill a count.
3. For each, establish what it costs: what it forces elsewhere, what it forecloses, how it fails.
4. Verify the specific behaviour and restrictions the approach depends on, using source, schemas, or official documentation for the relevant version. Existing code is evidence of its current use, not proof that a proposed variation is supported.
5. Separate established facts from remaining assumptions. Test decision-critical unknowns with a focused, reversible experiment before committing to the implementation; report a blocker if the necessary evidence is unavailable.

For a defect, Research is diagnosis: reproduce the failure or establish why it cannot be reproduced, and find the cause rather than the place the symptom surfaces. Establish a mechanism the evidence supports, that explains the observed behaviour, and that contradicts no known fact; code, logs, and traces can suffice where deterministic reproduction is unavailable. Where the evidence is insufficient, run focused diagnostics within the scope already authorised. Do not implement a speculative fix; report what remains unverified.

Stop when there is enough evidence to choose an approach. Involve the user only for the consequential decisions described below.

## Architecture

Goal: a decision, explicitly made.

1. After Research is complete, choose one approach and give the reason, in terms of the trade-offs Research found.
2. State what is being accepted: the cost, the limitation, the thing deliberately not solved.
3. Define the implementation: what changes where, in what order, and how it integrates with the existing code.
4. Define what would show the decision was wrong.

Reconcile the decision with all evidence from Research before implementation. A finding that invalidates the approach sends the work back to Research, not to the user: an approach can fail while another one still satisfies every constraint. Ask which constraint to relax only once the evidence establishes that the requirements cannot be satisfied together, and say what ruled the alternatives out. Ask first if the chosen approach requires an unapproved commitment, such as a dependency, migration, or behaviour change outside the request.

Scope this to the task. A local change needs a short paragraph, not a system design.

## Materialize

Implement the chosen approach.

- Follow the decision. If implementation requires changing the chosen approach, reconsider the decision explicitly instead of drifting into a different design.
- Follow the surrounding code's conventions, naming, and idiom, and preserve the required behaviour and contracts. Internal representations may change where that simplifies the solution within scope; existing structure is not itself a requirement.
- Build the simplest version that satisfies the requirements. Handle the input domain the change is responsible for, including what the existing schemas and contracts already admit; the examples in the request are not the specification. Do not add capability or abstraction for requirements that have not been stated.
- Keep the implementation coherent. Do not stack workarounds on a premise that is failing.

Return to Research when implementation shows that an assumption was invalid, a constraint was missed, or the chosen approach does not fit. On the direct path, this is how a task enters the RAM Cycle: say what changed.

Return to Foundation instead when the objective has to be restated — the problem, the expected outcome, or the boundary of what is being solved is not what it was taken to be. If the objective still stands and only the work needed to reach it grew, that is Research.

`references/ram-cycle.md` covers carrying evidence into a second pass, replacing a decision, and when to stop iterating. Read it once the cycle repeats or a decision from Architecture has to be replaced.

## Evaluate

Always performed. Depth matches risk and scope.

1. Check the original outcome, explicit constraints, and applicable external contracts. Passing checks establish only what they actually cover; file consistency alone does not prove preserved behaviour.
2. Exercise the behaviour that changed. Where existing tests already cover the regression, run them and name them; otherwise add or extend meaningful coverage. Check expected results independently of the implementation under test where shared logic could hide the same defect. For a failure that cannot be reproduced deterministically, test the mechanism that was changed. Where automated coverage is impractical or would only mirror implementation details, verify directly and report the coverage gap that remains.
3. Run the project's own checks for the affected areas: tests, type checking, linting, build. Find the real commands in the repository — package scripts, Makefile, CI configuration, tool configuration — instead of guessing. If they cannot be determined or cannot be run, say so plainly.
4. Read the diff for behaviour changes the user did not ask for, leftover debugging, dead code, and unhandled failure paths. Where tests were removed or weakened, establish which behaviour they protected: replace the coverage that mattered, and delete assertions that establish nothing.
5. Confirm that nothing depending on the previous behaviour was broken, starting with the callers and tests Foundation identified, and including the relevant boundary and failure paths. Where behaviour that had to survive the change is protected by no test, add one or name the gap. A fallback must satisfy the result contract or expose the failure explicitly; returning a value is not proof of success, and a check that gave up early has not established what it reports.

Do not let reading the diff stand in for running the change. Distinguish introduced failures from pre-existing or environmental failures; do not absorb unrelated fixes into the task. Name any behaviour that remains unverified.

If evaluation fails: an implementation defect returns to Materialize; an unsuitable approach or a newly discovered constraint returns to Research; a wrong understanding of the problem returns to Foundation.

## What to tell the user

Report engineering content, not stage transitions.

- On the direct path, do not narrate FRAME. Make the change, then report the result and the checks that were run.
- Surface reasoning where it carries something the user could disagree with: the approach chosen and its trade-off, an assumption that proved invalid, a task that turned out larger or different than it appeared, something the change deliberately does not solve.
- Keep Foundation and Research internal unless they changed the understanding of the task.
- Do not label messages with stage names or announce moving between stages. Name a stage only where it is the clearest way to explain a change of direction.
