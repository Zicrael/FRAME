# Case study: Fixing a Sudoku generator

A comparative test of FRAME against an unguided control run on a real codebase: same model, same prompt, same starting commit, two independent agents.

Both runs fixed the defect they were asked to fix. They diverged on a property of the original algorithm that the prompt never mentioned, and that is what decided the comparison.

## Setup

| | |
| --- | --- |
| Task | Fix a Sudoku generator that did not reliably respect the selected difficulty, while keeping puzzles valid and uniquely solvable |
| FRAME version | 1.1.0 |
| Starting state | Both runs branched from the same commit |
| Agent model | Cursor Grok 4.6 High |
| Reviewer | Claude 5 Opus High |
| Variables held constant | Model, prompt, repository state, tooling |

This comparison uses the original control run and a fresh run of FRAME after its instructions were refined using findings from earlier attempts on the same task. Intermediate development runs are omitted.

FRAME was evaluated on 50 generated puzzles per difficulty using an independent solver. Control measurements were taken from the earlier comparison in the same review session. Sizes and coverage come from the repositories and the coverage reporter rather than from generated puzzles.

## The deciding difference

The original algorithm removed clues in 180°-rotational pairs. This was deliberate and explicit — the function was named `removeCluesSymmetrically` and its docstring read *"Remove clues in batches (symmetry)"*. Symmetric givens are a classic Sudoku aesthetic property: the player sees it on every board. It was absent from the prompt because it was already part of the system's behaviour.

The control removed the symmetric removal strategy. Neither resulting test suite asserted symmetry, so passing tests did not expose the behavioural difference.

Fraction of givens whose 180°-mirrored cell is also a given:

| Difficulty (clues) | Control (no FRAME) | FRAME | Random chance |
| --- | ---: | ---: | ---: |
| Beginner (36) | 43% | 99.7% | 43.75% |
| Expert (24) | 26% | 87.2% | 28.75% |

The control's figures are close to the random-selection baseline at both ends of the range, indicating that the property was dropped rather than merely weakened.

## Scorecard

| Parameter | Control (no FRAME) | FRAME |
| --- | --- | --- |
| Rotational symmetry | **Lost** | **Largely retained** |
| Exact clue count, 4 difficulties | 100% of evaluated samples | 100% of evaluated samples |
| Unique solution | 100% of evaluated samples | 100% of evaluated samples |
| Reported token usage | 4.5M | 3.5M |
| Avg / worst generation, Expert | 16 ms / 53 ms | 25 ms / 77 ms |
| Generator line / branch coverage | 95.8% / 86.4% | 94.1% / 90.6% |
| Generator size | 243 lines | 273 lines |
| Component diff | 281 lines | 293 lines |

## Reading the results

**Both runs.** Each fixed a genuine latent bug: the original generator did not reliably reach its clue targets, and the original suite hid it behind `expect(nonZeroCells).toBeCloseTo(36, -3)`, a tolerance of roughly ±500 on an 81-cell board. Both hit the target exactly in every evaluated sample. Both validate puzzles in their own specs with a solver independent of the generator's search, and both mock the generator in the component spec so that the component test tests the component.

**Where the control was stronger.** It models the board as a flat `number[]` and derives row, column, and box from the index, eliminating the original's redundant `x` / `y` / `tile` fields — the cleaner data model of the two. It throws on a nonsense clue target, where the FRAME run silently returns a fully solved grid with nothing editable. It removed 11 tests that asserted nothing of value, one of them literally `expect(true).toBe(true)`. It is also faster, and 30 lines smaller.

**Where the FRAME run was stronger.** Beyond symmetry, it removed the redundant `table` ref from `SudokuWrapper.vue` — state that shadowed the store — and turned `fillRemainingNumbers` into a function taking the table as a parameter; that is what its extra 12 lines of component diff buy. Its generation fallback degrades to a board with more clues than requested, then to the last attempt, then throws, rather than returning a board it could not build. It replaced four difficulty tests that claimed to cover Beginner through Expert but never changed the difficulty before mounting, using a single loop with a fresh Pinia per case driven through the `changeGameDifficulty` action, and it targets the awkward branch directly with cases at 80 and 81 clues.

**Remaining limitation.** The FRAME implementation can report a puzzle as unique if its bounded solver stops after finding one solution without proving that a second solution does not exist. No violations were observed across 240 additional puzzles, but this remains a latent defect in the evaluated implementation.

An independent review by Claude 5 Opus High preferred the FRAME implementation overall. It retained substantially more of the original product behaviour while fixing the same defect, and used 22% fewer reported tokens in the selected run.

