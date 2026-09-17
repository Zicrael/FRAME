# Delegation

Experimental. FRAME runs as one agent unless a helper has a concrete contribution to make. Read this before the first handoff; it covers who owns what, what a handoff carries, and how a finding comes back.

## Who owns what

The skill establishes that the lead holds the requested outcome and answers for the result. What delegation adds:

**The lead** decides even where it did not investigate. Having delegated the question does not make the recommendation binding; implementation experience or the source itself can contradict it.

**The researcher** investigates the questions it was assigned and returns verified findings, the locations that support them, the uncertainty that remains, and a recommendation where the evidence supports one. It flags discoveries that change the understanding of the task even when the assignment did not ask about them.

**The validator** assesses the candidate against the original request and the contracts the work affects. It needs access to the underlying sources and the ability to run relevant checks. Its assessment covers incomplete delivery as well as regressions.

Helpers read anything, run checks, and set up isolated experiments within the authority the lead already has. Use at most one researcher and one validator alongside the lead.

## Handoff

A handoff is short and sufficient. It carries:

- the request and constraints that bear on the assignment, and the point at which the helper should stop;
- the source locations that matter, and the baseline or candidate under examination;
- what has been established as fact, kept separate from what is assumed;
- the question or decision that remains open;
- for validation, the candidate and the checks already run, including what they produced and which were blocked.

Point the helper at the underlying sources — files, tests, commands, documentation — so it can contradict a summary that turns out to be incomplete. Do not pass the conversation wholesale, and do not make each helper reload the whole methodology; the assignment carries what the role needs. A helper's summary informs the lead's understanding of the request; it never replaces the request.

When a handoff has to reference a FRAME document, use its path as installed alongside this skill. The project being worked on need not contain FRAME's own files.

## Validation

Validation assesses a stable candidate, and the two roles divide the effort instead of repeating it.

Before the handoff the lead runs the inexpensive checks available to it and repairs the straightforward failures its change introduced, so what it hands over is worth assessing rather than known breakage. A check that was blocked is passed on as blocked; that alone does not make the assessment pointless.

The validator chooses its own checks, concentrating on consequential risk and on the gaps rather than on ground already covered. It repeats one of the lead's checks when the evidence behind it is insufficient, when the candidate has changed since, or when running it independently would materially strengthen the assessment.

A finding states what requirement or behaviour is affected and the evidence for it, and distinguishes a demonstrated defect from a material verification gap and from an optional suggestion. Finding nothing is a valid result; no minimum count is expected. An assessment that ended early keeps the checks that completed and marks the rest as unverified — it is not an overall pass.

## Resolving findings

A helper's findings are resolved the same way as the lead's own, through the correction table in the skill. Send back only the finding or question that needs resolving, with the facts already established and the reasons an approach was rejected; one finding does not restart every role. A supported defect that prevents satisfying the request is repaired within the authority already granted — a narrow helper assignment does not exclude necessary work any more than an initial plan does.

The lead performs the recheck after its own repair, on the behaviour and findings that repair affects. Return to the validator when the repair changes enough that the earlier assessment no longer covers the candidate, or when the finding being repaired is one the lead's own evaluation had missed — a repair closed out only by the agent whose review missed the defect leaves the same blind spot in place. A recheck is not a second full assessment; it covers what the repair touched.
