# RAM Cycle

Research, Architecture, and Materialize repeat while uncertainty that could change the implementation decision remains. Read this once the cycle has turned at least once, or when a decision from Architecture has to be replaced.

## Re-entering Research

A second pass is not a repeat of the first. Carry the new information in:

- state what the last iteration established as fact and what it disproved;
- record why each rejected approach was rejected, and keep it rejected for as long as that reason holds. Evidence or a constraint that removes the reason — a dependency since authorised, a limitation since disproved — puts the approach back in scope;
- check whether the reason the previous approach failed also invalidates the alternatives that were considered next best.

A return that arrives from a delegated finding carries the same material: the assumption that failed, the evidence that failed it, and the rejection reasons that still apply. See [delegation.md](delegation.md).

Before another experiment, name the unresolved question and how its answer would change the decision. Re-research only the part that moved. Reopen a settled question when its premise changed, and say what changed. Difficulty on its own neither reopens a settled question nor restarts the workflow.

## Revising the decision

Say which decision is being replaced and why. The record of what was tried and rejected is what stops the cycle from circling.

Keep the accepted trade-offs current. If the new approach accepts a cost the previous one did not, that is user-facing.

## Stopping

Leave the cycle for Evaluate when the remaining unknowns no longer change the implementation decision. Residual uncertainty that Evaluate can measure is not a reason to prolong Research.

When the same class of failure returns, reassess the diagnosis and approach. Continue with a focused experiment when new evidence supports a next hypothesis. Return to Foundation if the evidence changes the understanding of the problem; otherwise apply the stopping conditions below.

Stop and involve the user when:

- investigation has stopped producing evidence, and the next step would be a variation without a hypothesis. Trying variations is not Materialize;
- progress depends on information, access, or a judgement that is not available to you;
- every viable approach requires a commitment beyond the authority the request and the applicable project rules already grant, such as a new dependency, a behaviour change, a migration, or a performance cost;
- the stated constraints are contradictory.

## Recurring failures

- Skipping Research on the second pass and reimplementing on intuition.
- Treating an unverified assumption as established because it survived one iteration.
- Widening scope each turn. The task is still the one Foundation established.
- Repairing the symptoms of a wrong approach instead of replacing the approach.
