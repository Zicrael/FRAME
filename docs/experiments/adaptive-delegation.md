# Adaptive Delegation

**Status: experimental. No results have been measured yet.**

FRAME runs as a single agent by default. This experiment tests whether letting that agent optionally delegate a bounded research question, or hand a candidate change to an independent validator, produces better engineering outcomes at an acceptable cost. The methodology and the RAM Cycle are unchanged; delegation only affects who carries out a responsibility.

The definitions under test are the routing rules in the FRAME skill, the coordination policy in `skills/frame/references/delegation.md`, and the two role definitions in `agents/`.

## Hypotheses

1. **Validation finds defects that self-review misses.** An agent that did not write the change detects defects the implementing agent's own evaluation does not, because it does not inherit the implementation's assumptions.
2. **The gain comes from independence, not from extra effort.** A separate validator outperforms the same amount of additional verification performed by the implementing agent itself. If it does not, the extra agent is not paying for itself.
3. **Research delegation helps only on suitable tasks.** Delegating a bounded, separable investigation improves the implementation decision on tasks that contain one, and adds cost without improving outcomes on tasks that do not.
4. **Routing is cheap when it declines.** Because the default is one agent, the routing rules add little cost on tasks where no helper is warranted.

Each hypothesis is falsifiable by the measurements below. A hypothesis that the data does not support is recorded as unsupported rather than reworded.

## Routing criteria

Routing has to be observable, so that a run can be classified after the fact and disagreement about it can be resolved. For each run, record the arrangement chosen and the criterion the lead cited:

| Decision | Recorded criterion |
| --- | --- |
| Research delegated | The question named, why its answer could change the implementation decision, and which of separate context, specialised investigation, or separable exploration applied |
| Research not delegated | Either no question could change the decision, the investigation was not separable from the implementation, or the lead could resolve it directly for less expected work |
| Validation added | The consequential behaviour that remained weakly verified, or the assumption a separate assessment could challenge, and what follows if it is wrong |
| Validation not added | Why the change's consequential behaviour is adequately verified by the lead's own evaluation |

Task size, file count, uncertainty alone, confidence alone, and the importance of the task alone are not routing criteria. A run whose recorded justification appeals to one of them, or that delegates without a useful assignment, is a routing error, and is counted as such whether or not the outcome was correct.

## Comparison

The headline comparison is the definitions as shipped against the same definitions with delegation taken away:

| Arm | Description |
| --- | --- |
| **A. Adaptive FRAME** | The definitions as shipped. The lead chooses among all four arrangements for itself, including choosing to stay alone. |
| **B. Delegation disabled** | The same definitions, with no helper available, so the lead carries every responsibility itself. This is the control. |

The difference between A and B is the effect of adaptive delegation with its routing decisions included. A run in which the lead declines to delegate is still an arm A run, and the cost of reaching that decision belongs to the routing rules.

The fixed arrangements explain a result rather than produce the headline number. Run them on the tasks where A and B diverge, or where the recorded routing looks wrong:

| Diagnostic arm | What it isolates |
| --- | --- |
| **C. Single agent, extra verification** | One agent instructed to verify further itself, separating independence from effort (hypothesis 2). |
| **D. Lead and validator, always** | Whether validation would have helped where the lead declined it, and what it costs where the lead chose it. |
| **E. Research delegated, always** | Whether the delegated question was the useful one, on tasks that contain a separable investigation and on tasks that do not. |

Arm C is given a comparable additional budget to arm D, so that the comparison is between independence and effort rather than between more work and less.

## Controls

Held fixed across arms for a given task:

- repository revision and starting working tree;
- task prompt, verbatim;
- model, effort, and any other model settings, for the lead and for every helper;
- available tooling, including MCP servers, network access, and permissions;
- total compute budget for the run, counted across all agents rather than per agent.

Any control that could not be held is recorded with the run, and the run is reported separately rather than pooled.

## Accounting

Usage is counted for the run as a whole:

- tokens and requests for every agent, including helpers;
- every handoff, in both directions;
- repairs performed after a finding;
- checks that were run more than once, including rechecks after a repair.

A per-agent figure that omits helpers, handoffs, or repeated checks is not a cost measurement for the run and is not used as one.

### Finding disposition

Keep every helper assignment and every return, and record for the run:

- which material findings reached the lead;
- which of them prompted a repair;
- which were rejected or left blocked, and the reason given;
- what was rechecked afterwards, and what the recheck produced.

A required defect that was reported but left unresolved is counted apart from a defect nobody reported. The first is a resolution failure and the second a detection failure, and pooling them hides which part of the arrangement broke down.

This accounting belongs to the benchmark. An ordinary FRAME task adds no reporting on top of the result, the relevant checks, and the material limitations the skill already asks for.

## Measurements

Per run:

- **Correct completion** — the requested outcome achieved, judged against the original task.
- **Preserved behaviour** — behaviour and contracts that had to survive, still intact.
- **Missed defects** — defects present at the end of the run that the arm's own verification did not report.
- **Unresolved required defects** — defects that were reported, required repair, and were still unfixed when the run ended, with the reason recorded.
- **Incorrect findings** — reported findings that are not defects, and the effort spent resolving them.
- **Billed cost** — the accounting above, in the units the provider bills.
- **Elapsed time** — wall-clock time to completion, which differs from cost where agents run concurrently.

The benchmark's final assessment is performed separately from the workflow's own validator, by a judge that is not part of the run and does not see which arm produced a candidate. A validator's report is data about the arm, never the verdict on it.

## Protocol

Arms A and B run repeatedly on every task; a single run is not a result. The diagnostic arms run repeatedly on the tasks they were selected for, and their results are reported as explanations of specific tasks rather than pooled with the headline comparison. Tasks are drawn from work the definitions were not written against, and are added rather than replaced, so that a task cannot be tuned for after it has been used.

Coverage the task set has to include:

- tasks that elicit each of the four arrangements from arm A: lead alone, lead and researcher, lead and validator, lead with both;
- tasks where delegation is unavailable or disallowed, checking that the lead carries the responsibility itself and reports the verification it actually performed;
- targeted follow-ups after a finding, checking that only the relevant question or finding returns and that the other roles are not restarted.

## Results

Pending. Nothing in this document has been measured yet, and no claim about quality, cost, or speed should be drawn from it until the runs above have been carried out and reported here.
