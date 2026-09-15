# Delegation

Experimental. FRAME runs as a single agent unless there is a reason not to. Read this before the first delegation. It defines how a lead works with helpers so that the methodology stays the same when its responsibilities are shared.

## Arrangements

Four staffings are supported: the lead alone, lead and researcher, lead and validator, or lead with both. For this experiment use at most one researcher and one validator alongside the lead, and reuse the same helper for a focused follow-up rather than starting another one. Helpers do not delegate further.

The lead is the only agent that writes production code. Helpers read anything, run checks, and set up isolated experiments within the authority the lead already has.

## Handoff

A handoff is short and specific. It states:

- the objective assigned, its scope, and the condition under which the helper should stop;
- the original requirements and the constraints that bear on them;
- the source locations that matter, and the baseline or candidate under examination;
- what has been established as fact, which decisions were consequential, and which questions remain open;
- which checks have already run, and what they actually produced.

Keep established evidence separate from assumption, and mark anything believed but unverified. Point the helper at the underlying sources — files, tests, commands, documentation — so that it can contradict a summary that turns out to be incomplete. Do not copy the conversation wholesale, and do not make each helper reload the whole methodology; the assignment carries what the role needs.

When a handoff has to point at a FRAME reference, use the path of the file as installed alongside this skill. The project being worked on need not contain FRAME's own files.

## Validation

Validation assesses a stable candidate. When the lead changes the code afterwards, the findings and behaviour that change affects have to be rechecked.

## Resolving findings

A finding re-enters the workflow where its cause lies:

- an implementation defect returns to Materialize;
- an invalid assumption or an unsuitable approach returns to Research;
- a misunderstood outcome or constraint returns to Foundation.

Carry the established facts and the reasons an approach was rejected into that transition, and send back only the question or finding that needs resolving. One finding does not restart every role.

## Stopping

Stop when the task and the checks that matter are satisfied. Going further needs a concrete unresolved risk, a hypothesis worth testing, or a check that has not run. An assessment that stopped early, was blocked, or never finished establishes nothing; report it as what it was rather than as a pass.
