# Changelog

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
