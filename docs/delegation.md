# Delegation

FRAME names five responsibilities; it does not require five participants. This document covers when another agent is worth involving and how its findings come back. The operational instructions agents follow during a handoff are in [`skills/frame/references/delegation.md`](../skills/frame/references/delegation.md).

## One lead by default

Every task starts with one accountable lead carrying all five responsibilities: it holds the requested outcome, decides the approach, implements it, resolves findings, and answers for the result. A helper joins only when it has a concrete contribution to make, because each one costs a handoff and the context it has to rebuild.

Two roles exist: a **researcher** resolves assigned questions and returns findings with the sources behind them, and a **validator** assesses a candidate against the original request and reports defects, omitted required work, and verification gaps. Helpers write no production code and do not delegate further.

## Arrangements

| Arrangement | When it fits |
| --- | --- |
| Lead alone | The lead can understand, perform, and meaningfully verify the work itself. |
| Lead and validator | A separate assessment could expose consequential mistakes, omissions, or unsupported assumptions. |
| Lead and researcher | A substantial investigation benefits from its own context. |
| Lead, researcher, and validator | The investigation separates usefully and the implementation also earns an independent check. |

Research and validation are independent choices: delegating the investigation does not commit the lead to delegating the assessment. Where subagents are unavailable, the lead carries every responsibility itself and reports the verification it actually performed.

## Choosing

What decides it is what a helper would add against what coordinating it costs: the uncertainty a separate investigation would resolve, the consequences of the change going wrong, and whether verification needs an assessment the lead cannot give its own work. Task size and file count do not decide it, the arrangement may change as evidence develops, and the choice should stay a quick judgment. FRAME makes no claim that adding an agent improves quality, speed, or cost.

## How findings return

A finding re-enters the work where its cause lies. An implementation defect or omitted required work goes back for repair, followed by a recheck of what the repair affects. An invalid assumption or unsuitable approach returns to the relevant investigation and the decision built on it. Neither restarts the whole task, and a finding does not have to travel through research to be fixed.

## Completion

The lead integrates the findings and remains responsible for delivery. It evaluates its own work in every arrangement — an independent validator adds a second assessment rather than replacing the lead's — and accounts for material findings before reporting completion: a required defect left unrepaired is not complete.
