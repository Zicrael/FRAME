# RAM Cycle

Research, Architecture, and Materialize repeat while meaningful uncertainty remains. Read this once the cycle has turned at least once, or when a decision from Architecture has to be replaced.

## Re-entering Research

A second pass is not a repeat of the first. Carry the new information in:

- state what the last iteration established as fact and what it disproved;
- keep ruled-out approaches ruled out;
- check whether the reason the previous approach failed also invalidates the alternatives that were considered next best.

Re-research only the part that moved. Do not reopen settled questions.

## Revising the decision

Say which decision is being replaced and why. The record of what was tried and rejected is what stops the cycle from circling.

Keep the accepted trade-offs current. If the new approach accepts a cost the previous one did not, that is user-facing.

## Stopping

Leave the cycle for Evaluate when the remaining unknowns no longer change the design. Residual risk that Evaluate can measure is not a reason to keep iterating.

Stop and involve the user when:

- the same class of failure returns after a revision, which usually means the problem is framed wrong — return to Foundation;
- every viable approach requires accepting something the user has not agreed to, such as a new dependency, a behaviour change, a migration, or a performance cost;
- the stated constraints are contradictory;
- work has become guess-and-check. Trying variations without a hypothesis is not Materialize.

## Recurring failures

- Skipping Research on the second pass and reimplementing on intuition.
- Treating an unverified assumption as established because it survived one iteration.
- Widening scope each turn. The task is still the one Foundation established.
- Repairing the symptoms of a wrong approach instead of replacing the approach.
