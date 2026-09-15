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

Four arms run on the same tasks:

| Arm | Description |
| --- | --- |
| **A. Compact single-agent FRAME** | The skill's baseline, no delegation. This is the control. |
| **B. Single agent, extra verification** | One agent, instructed to perform additional verification itself. Separates independence from effort (hypothesis 2). |
| **C. Lead and validator** | The lead implements; a separate validator assesses the candidate. |
| **D. Research delegation** | The lead delegates a bounded question, on tasks that contain one and on tasks that do not, so that the cost of a wrong routing decision is visible too. |

Arm B is given a comparable additional budget to arm C, so that the comparison is between independence and effort rather than between more work and less.

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

## Measurements

Per run:

- **Correct completion** — the requested outcome achieved, judged against the original task.
- **Preserved behaviour** — behaviour and contracts that had to survive, still intact.
- **Missed defects** — defects present at the end of the run that the arm's own verification did not report.
- **Incorrect findings** — reported findings that are not defects, and the effort spent resolving them.
- **Billed cost** — the accounting above, in the units the provider bills.
- **Elapsed time** — wall-clock time to completion, which differs from cost where agents run concurrently.

The benchmark's final assessment is performed separately from the workflow's own validator, by a judge that is not part of the run and does not see which arm produced a candidate. A validator's report is data about the arm, never the verdict on it.

## Protocol

Each arm runs repeatedly on each task; a single run of an arm is not a result. Tasks are drawn from work the definitions were not written against, and are added rather than replaced, so that a task cannot be tuned for after it has been used.

Coverage the task set has to include:

- all four arrangements: lead alone, lead and researcher, lead and validator, lead with both;
- tasks where delegation is unavailable or disallowed, checking that the run completes as a single agent and reports the verification it actually performed;
- targeted follow-ups after a finding, checking that only the relevant question or finding returns and that the other roles are not restarted.

## Results

Pending. Nothing in this document has been measured yet, and no claim about quality, cost, or speed should be drawn from it until the runs above have been carried out and reported here.
