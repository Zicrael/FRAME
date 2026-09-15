# Delegation

Experimental. FRAME runs as a single agent unless there is a reason not to. Read this before the first delegation. It defines how a lead works with helpers so that the methodology stays the same when its responsibilities are shared.

## Arrangements

Four staffings are supported: the lead alone, lead and researcher, lead and validator, or lead with both. For this experiment use at most one researcher and one validator alongside the lead, and reuse the same helper for a focused follow-up rather than starting another one. Helpers do not delegate further.

Research assignments go to `frame-researcher`, validation assignments to `frame-validator`. Resolve each identifier as the host exposes it, including any plugin namespacing. When the helper a responsibility calls for is unavailable, the lead carries out that responsibility itself.

The lead is the only agent that writes production code. Helpers read anything, run checks, and set up isolated experiments within the authority the lead already has.

## Handoff

A handoff is short and specific. It states:

- the objective assigned, its scope, and the condition under which the helper should stop;
- the original requirements and the constraints that bear on them;
- the source locations that matter, and the baseline or candidate under examination;
- what has been established as fact, which decisions were consequential, and which questions remain open;
- which checks have already run, what they actually produced, and which gaps remain.

Keep established evidence separate from assumption, and mark anything believed but unverified. Point the helper at the underlying sources — files, tests, commands, documentation — so that it can contradict a summary that turns out to be incomplete. Do not copy the conversation wholesale, and do not make each helper reload the whole methodology; the assignment carries what the role needs.

When a handoff has to point at a FRAME reference, use the path of the file as installed alongside this skill. The project being worked on need not contain FRAME's own files.

## Validation

Validation assesses a stable candidate, and the two roles divide the effort rather than repeating it.

Before the handoff, the lead runs the inexpensive, relevant checks already available to it and repairs the straightforward failures its change introduced, so that what it hands over is a candidate worth assessing rather than known breakage. A check that was blocked is passed on as blocked; on its own that does not make the review pointless.

The validator chooses its own checks, concentrating on consequential risks and on the gaps rather than on ground the lead has already covered. It repeats an existing check when the evidence behind it is insufficient, when the candidate has changed since, or when running it independently would materially strengthen the assessment.

When the lead changes the code afterwards, the findings and behaviour that change affects have to be rechecked.

## Resolving findings

Before completion, the lead resolves material researcher and validator findings against the original outcome and affected contracts. Supported defects that prevent satisfying them require repair and affected checks within the authority already granted; an initial plan or helper assignment does not exclude necessary work. Defects left unfixed need an evidence-based reason: unsupported, outside the requested scope, or blocked. A blocked required repair means the task remains incomplete.

A finding re-enters the workflow where its cause lies:

- a material verification gap returns to Evaluate for the smallest practical check; missing evidence alone is not a demonstrated defect;
- an implementation defect returns to Materialize;
- an invalid assumption or an unsuitable approach returns to Research;
- a misunderstood outcome or constraint returns to Foundation.

Carry the established facts and the reasons an approach was rejected into that transition, and send back only the question or finding that needs resolving. One finding does not restart every role.

## Stopping

Stop when the task and the checks that matter are satisfied. Going further needs a concrete unresolved risk, a hypothesis worth testing, or a check that has not run.

An assessment that ended early still carries weight. Preserve the checks that completed and the findings the evidence supports, and mark the unfinished checks and the behaviour they would have covered as unverified. An incomplete assessment is not an overall pass. A focused follow-up starts from that evidence instead of repeating work already done.
