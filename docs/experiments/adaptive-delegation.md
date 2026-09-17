# Adaptive Delegation

**Status: experimental. No results have been measured yet.**

This experiment tests two things that the current revision changed together: instructions led by the requested outcome rather than by a fixed process, and a lead agent that may optionally delegate an investigation or an independent assessment. Both are hypotheses. Nothing here establishes that FRAME, or an additional agent, improves quality or reduces cost.

The definitions under test are the five responsibilities and the routing guidance in the FRAME skill, the coordination policy in `skills/frame/references/delegation.md`, and the two role definitions in `agents/`.

## Hypotheses

1. **Outcome-led instructions scale the work.** Instructions that derive effort from the requested outcome and its uncertainty spend less on straightforward tasks than the process-led revision they replace, without omitting required work on broad ones. Both failure directions are measured, because simplification can just as easily produce under-delivery. The comparative half of this hypothesis needs arm 1p below; the arms that test delegation cannot establish it.
2. **Validation finds defects that self-review misses.** An agent that did not write the change detects defects the implementing agent's own evaluation does not, because it does not inherit the implementation's assumptions.
3. **The gain comes from independence, not from extra effort.** A separate validator outperforms the same additional verification effort spent by the implementing agent itself. If it does not, the extra agent is not paying for itself.
4. **Research delegation helps only on suitable tasks.** Delegating a substantial, separable investigation improves the implementation decision on tasks that contain one, and adds cost without improving outcomes on tasks that do not.
5. **Routing is cheap when it declines.** Because the default is one agent, the routing guidance adds little cost on tasks where no helper is warranted.
6. **Findings are resolved, not deferred.** Material findings that require repair are repaired and rechecked before completion, rather than reported as residual issues.

Each hypothesis is falsifiable by the measurements below. A hypothesis the data does not support is recorded as unsupported rather than reworded.

## Comparison

Four arms, each adding one thing to the one before it. The interesting quantities are the differences between adjacent arms:

| Arm | Configuration | Difference from the arm above |
| --- | --- | --- |
| **0. No FRAME** | The same task prompt with no FRAME instructions. | Control for the methodology itself. |
| **1. FRAME, delegation unavailable** | The revised instructions, no helper available, so the lead carries every responsibility. | The effect of the instructions alone (1 − 0). |
| **2. FRAME, validation available** | `frame-validator` available; the lead decides whether to use it. | The additional effect of independent validation (2 − 1). |
| **3. FRAME as shipped** | Both helpers available; the lead chooses among all supported arrangements. | The additional effect of research delegation (3 − 2). |

Arm 0 is the control for the methodology as a whole, and arm 1 is the control for *using* a helper. Arm 1 is not a control for the routing guidance itself: the Participants section is part of the instructions arm 1 reads, so it pays the cost of considering a helper and declining. Record how unavailability was enforced — helpers absent from the installation with the instruction text unchanged is what a host without subagents actually looks like, and is the configuration to use unless a run states otherwise. Hypothesis 5 therefore rests on the absolute routing cost measured below rather than on any difference between arms, so fix the threshold that would count as "little cost" before the runs rather than after.

A run in which the lead declines to delegate is still a run of its arm, and the cost of reaching that decision belongs to the routing guidance. Arm 3 is the shipped configuration, so its result is the one users experience; the differences explain where that result comes from.

Hypothesis 1 needs one further arm, which is not part of the nesting:

| Arm | Configuration | Difference it supports |
| --- | --- | --- |
| **1p. Prior revision** | The instruction set this revision replaced, at commit `7e950fe`, with no helper available. | The effect of the rewrite itself (1 − 1p). |

Without 1p, no difference between arms can order the revised instructions against the ones they replaced: 1 − 0 compares having instructions with having none, which says nothing about whether the rewrite reduced cost or increased omissions. Arm 1 alone shows only whether the new instructions are cheap, not whether they are cheaper.

The remaining arms explain a result rather than produce a headline number. Run each of them on a fixed sample of every task category, and additionally wherever adjacent arms diverge or the recorded routing looks wrong. Divergence cannot be the trigger on its own: where the lead consistently declines a helper, the adjacent arms converge, and whether that helper would have helped is precisely what the forced arm answers.

| Diagnostic arm | What it isolates |
| --- | --- |
| **1b. Single agent, extra verification** | One agent instructed to verify further itself, separating independence from effort (hypothesis 3). |
| **2b. Validation forced** | Whether validation would have helped where the lead declined it, and what it costs where the lead chose it. |
| **3b. Research delegation forced** | Whether the delegated question was the useful one, on tasks that contain a separable investigation and on tasks that do not. |

Arm 1b is given a comparable additional budget to arm 2b, so that the comparison is between independence and effort rather than between more work and less.

## Routing observations

Routing has to be observable, so that a run can be classified after the fact and disagreement about it can be resolved. For each run, record the arrangement chosen and the reason the lead cited:

| Decision | Recorded reason |
| --- | --- |
| Research delegated | The question assigned, and the concrete contribution that justified the handoff and the context the helper had to rebuild |
| Research not delegated | Either no question was substantial enough to separate, or the lead could resolve it directly for less expected work |
| Validation added | The consequential mistake, omission, or assumption a separate assessment could expose, and what follows if it is wrong |
| Validation not added | Why the lead's own evaluation verifies the consequential behaviour adequately |

Task size, file count, uncertainty alone, confidence alone, and the importance of the task alone are not routing reasons. A run whose recorded justification appeals to one of them, or that delegates without a useful assignment, is a routing error and is counted as such whether or not the outcome was correct.

Record arrangement changes during a run as well as the initial choice, since the arrangement is allowed to change as evidence develops.

## Controls

Held fixed across arms for a given task:

- repository revision and starting working tree;
- task prompt, verbatim;
- model, effort, and any other model settings, for the lead and for every helper;
- available tooling, including MCP servers, network access, and permissions;
- rule activation state. Arm 0 requires `rules/frame.mdc` to be absent rather than merely unused, since it is `alwaysApply: true`.

Compute is capped per run, at a ceiling set high enough that no arm reaches it, and is then measured rather than equalised. Holding a single total fixed across arms with different agent counts would make the lead spend less whenever a helper spends anything, turning the difference between adjacent arms into an effect of reallocating a fixed budget rather than of adding an assessment or an investigation. A run that does reach the ceiling is reported separately. The one place a budget is deliberately matched is arm 1b against arm 2b, where the question is independence against effort.

Any control that could not be held is recorded with the run, and the run is reported separately rather than pooled.

## Accounting

Usage is counted for the run as a whole:

- tokens and requests for every agent, including helpers;
- every helper actually invoked, and every handoff in both directions;
- repairs performed after a finding;
- checks that were run more than once, including rechecks after a repair.

A per-agent figure that omits helpers, handoffs, or repeated checks is not a cost measurement for the run and is not used as one.

### Finding disposition

Keep every helper assignment and every return, and record for the run:

- which material findings reached the lead;
- which of them prompted a repair, and what the recheck afterwards produced;
- which were rejected or left blocked, and the reason given;
- which required defects were reported and still shipped as residual issues (hypothesis 6).

A required defect that was reported but left unresolved is counted apart from a defect nobody reported. The first is a resolution failure and the second a detection failure; pooling them hides which part of the arrangement broke down.

This accounting belongs to the benchmark. An ordinary FRAME task adds no reporting beyond the result, the relevant checks, and the material limitations the skill already asks for.

## Measurements

Per run:

- **Correct completion** — the requested outcome achieved, judged against the original task.
- **Omitted required work** — work the request needed that the deliverable does not contain, whether or not what it does contain is correct.
- **Preserved behaviour** — behaviour and contracts that had to survive, still intact.
- **Missed defects** — defects present at the end of the run that the arm's own verification did not report.
- **Unresolved required defects** — defects that were reported, required repair, and were still unfixed when the run ended, with the reason recorded.
- **Incorrect findings** — reported findings that are not defects, and the effort spent resolving them.
- **Process overhead on straightforward tasks** — cost spent on investigation, coordination, and routing on tasks whose deliverable did not need it (hypotheses 1 and 5).
- **Billed cost** — the accounting above, in the units the provider bills.
- **Elapsed time** — wall-clock time to completion, which differs from cost where agents run concurrently.

The benchmark's final assessment is performed separately from the workflow's own validator, by a judge that is not part of the run and does not see which arm produced a candidate. A validator's report is data about the arm, never the verdict on it.

## Protocol

Arms 0 through 3 run repeatedly on every task; a single run is not a result. The diagnostic arms run repeatedly on the tasks they were selected for, and their results are reported as explanations of specific tasks rather than pooled with the headline comparison. Tasks are drawn from work the definitions were not written against, and are added rather than replaced, so that a task cannot be tuned for after it has been used.

Coverage the task set has to include:

- each deliverable shape the instructions distinguish: a straightforward change, a request whose deliverable is findings, a diagnosis followed by a fix, and a broad improvement request;
- tasks that elicit each arrangement from arm 3: the lead alone, lead and validator, lead and researcher, and lead with both;
- tasks where a helper is unavailable or disallowed, checking that the lead carries the responsibility itself and reports the verification it actually performed;
- tasks where evidence should expand the initial plan, checking that necessary related work is included and optional improvements are not;
- a validator finding that requires another implementation pass, checking that the repair and its recheck happen before completion and that the other responsibilities are not restarted.

Do not draw conclusions from instruction review alone. Reasoning about how the definitions should behave on these cases is design work, not evidence; only executed runs count as results.

## Results

Pending. Nothing in this document has been measured yet, and no claim about quality, cost, or speed should be drawn from it until the runs above have been carried out and reported here.
