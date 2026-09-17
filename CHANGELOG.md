# Changelog

## Unreleased

Experimental revision of the methodology, the skill, and the agent instructions. It replaces the accumulated process guidance with an outcome-led methodology and should be treated as a hypothesis to test, not as an improvement. Nothing here has been measured; no claim is made about quality, cost, or speed. Installation, packaging, and version bumps are unchanged.

- Guiding principle: FRAME guides engineering judgment. The requested outcome determines the work; uncertainty and verification needs determine the effort and the participants. The FRAME name, the `frame` skill identifier, and "Consideration before Implementation" are unchanged.
- **A** is now **Align**, replacing Architecture: assess the approach against the real implementation context and decide how to proceed, examining the evidence when research was delegated. It is an engineering decision rather than a mandatory human approval gate.
- The five letters are described as responsibilities rather than stages. They do not require five conversations, reports, or rigidly ordered passes; Research and Align can be brief when the approach is already clear.
- Work scales to the requested deliverable. A straightforward change goes from understanding to implementation and verification; a request whose deliverable is findings finishes with supported findings and no code; a diagnosis-and-fix request includes both; a broad request gets enough investigation and implementation to reach its outcome. The initial plan stays revisable when evidence shows the outcome needs related work, and the requested outcome is not weakened to make a candidate pass.
- The RAM Cycle is removed as a separately named cycle, along with `skills/frame/references/ram-cycle.md`. The behaviour behind it is kept where it informs a decision: investigate a failed attempt before replacing the approach, carry established evidence forward, keep the reason each rejected alternative was rejected, and name the question the next attempt would answer.
- Delegation is adaptive rather than staged, starting from one accountable lead. Three common arrangements are described — one agent carrying FRAME, an FRAM lead with independent E, and an FR researcher with an AM lead and an E validator — and either helper may be used without the other, so delegating the investigation does not commit the lead to delegating the assessment. The letters show where the effort falls, not where accountability moves: the lead holds the requested outcome throughout and evaluates its own work in every arrangement, and an independent validator adds a second assessment rather than replacing the lead's. Task size and file count do not decide agent count. Where a helper is unavailable, the lead carries the responsibility itself and reports the verification actually performed.
- `skills/frame/references/delegation.md` is simplified to role ownership, what a handoff carries, how the lead's checks and independent validation divide the effort, and how findings are resolved. Handoffs carry the request, source pointers, established findings, the open question, and the candidate with its checks; they do not carry the conversation or the whole methodology.
- Correction is focused: a defect or omission is repaired and rechecked, an invalid assumption returns to the relevant investigation, a misunderstood outcome is corrected against the original request, and a verification gap is closed by the smallest practical check. Not every finding travels through Research. The lead performs the recheck, and returns to the validator when the repair outdates the earlier assessment or when the finding is one the lead's own evaluation had missed. Before completion the lead accounts for material findings; reporting an actionable required defect as a residual issue does not repair it.
- `frame-researcher` and `frame-validator` are aligned with the revised responsibilities: the researcher returns findings with source locations, consequential assumptions, and a supported recommendation; the validator assesses the candidate against the original request and reports omitted required work alongside regressions. Helpers write no production code and do not delegate further.
- The always-applied rule now also activates on substantive engineering investigation, such as diagnosing a defect or establishing how a dependency behaves, and keeps the exception for agents acting on a FRAME helper assignment.
- Iteration keeps the stop conditions the removed cycle carried: check whether the reason an approach failed also rules out the alternative about to replace it, reassess the diagnosis when the same kind of failure returns, and report the blocker instead of varying further once investigation stops producing evidence.
- Documentation: the README and [Workflow](docs/workflow.md) describe the responsibilities, scaling, and iteration without a named cycle; [Principles](docs/principles.md) is adjusted for consistency. [Adaptive delegation](docs/experiments/adaptive-delegation.md) now separates the effect of the instructions from the effects of independent validation and research delegation, keeps a no-FRAME control, adds an arm running the instruction set this revision replaced so the rewrite itself can be compared, measures compute rather than holding a shared budget fixed across arms with different agent counts, and records omitted required work alongside total cost across all agents.
- The README states that the case-study token figures record two particular runs rather than a measured saving, including that the FRAME run followed instruction refinements made on that same task while the control did not.

## 1.1.1 — 2026-09-15

- Plugin version is `1.1.1`.
- FRAME is now also a Claude Code plugin.

## 1.1.0 — 2026-09-14

- Plugin version is `1.1.0`.
- Foundation identifies the behaviour and contracts that must survive the change, including those the request omits, and distinguishes intended behaviour from defects. Materialize preserves those contracts; internal representations may change where that simplifies the work in scope.
- Follow-ups inherit Foundation. Diagnosis, investigation, and user involvement stay with the evidence: involve the user only for authority, conflicting requirements, or unavailable information; a failed approach is a reason to investigate further, not to stop.
- Evaluate checks results independently where shared logic could hide the same defect, adds coverage or names the gap when preserved behaviour has no test, and requires fallbacks and incomplete checks to report only what they actually established.
- RAM Cycle: a failed approach goes back to Research; repeated failure triggers reassessment, not automatic escalation; a rejected approach reopens when the reason it was rejected no longer holds.
- README replaces the early token-usage table with Case studies. First comparison: a Sudoku generator fix against a control run on a real codebase.

## 1.0.0 — 2026-09-12

- Plugin version is `1.0.0`.
- README install path leads with Cursor Directory; local copy remains available from the repo.
- Document the always-applied rule, `/frame` usage, support, and that FRAME collects no data.
- Early results keep the original test table and describe them as initial observations, not a guaranteed saving.
- LICENSE copyright matches the plugin author.

## 0.2.0 — 2026-09-12

- Plugin version is `0.2.0`.
- FRAME skill: treat user constraints as acceptance criteria; verify behaviour before committing to an approach; Evaluate against the original outcome.
- README: shorter positioning, RAM Cycle / direct path, early results, and local plugin install.

## 0.1.0 — 2026-09-11

- Initial Cursor plugin: manifest, always-applied rule, FRAME skill, and branding.
- Methodology docs (principles and workflow) shipped in the same tree. There was no git tag for this version.
