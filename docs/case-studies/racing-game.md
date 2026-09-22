# Case study: Rewriting a browser racing game

A comparative test of FRAME against an unguided control run: same rewrite prompt, two independent implementations of a browser mini-game, then a review that did not receive method labels.

Both runs produced a Vue 3, TypeScript, and Vite game that could start, dodge, score, pause, crash, restart, and keep a best score. They diverged on whether essential gameplay stayed visible in the reviewed short-height viewports, and that is what decided the comparison.

This was one paired comparison, not an estimate of FRAME’s average effect. It does not isolate the contribution of the core instructions from delegated research or validation.

## Setup

| | |
| --- | --- |
| Task | Rewrite an existing two-lane race game as a finished browser mini-game on Vue 3, TypeScript, and Vite, keeping two-lane movement, oncoming cars, score, a persistent best, start / lose / restart, pause with resume, gradual difficulty, keyboard and touch controls, and obstacles that leave an achievable dodge |
| FRAME version | 2.0.0 experimental (documentation tree this study is filed in). The instruction revision used by the FRAME implementation run was not recorded |
| Agent model | Cursor Grok 4.6 High |
| Reviewer | GPT-6 Astra High / Cursor Grok 4.6 Extra High |
| Scoring | Functionality 40, code quality 30, visuals and usability 30 |
| Variables held during review | Neither implementation was modified. Method labels were withheld. Extra features, file counts, and extra tests were not rewarded unless they improved the requested result. Defects were scored separately from preferences |

The prompt also required studying the existing game, fixing defects that blocked the requirements or normal play, choosing structure and rendering, using or replacing assets, staying fully client-side, shipping `npm run dev` and `npm run build`, updating the README, and checking collisions, pause, several restarts, and best-score persistence — with automatic checks and a browser pass when a browser was available.

Passing tests were treated as insufficient on their own. The review inspected source, ran `npm test` and `npm run build` for both trees, played the required scenarios in the browser, and compared matching viewport sizes and game states, including short-height screenshots from the requester.

Withholding method labels is a strength of the review. The later score change is a re-evaluation by the same reviewer after new screenshots, not a second independent experiment.

## The deciding difference

The brief required the game to play comfortably with a keyboard and with on-screen controls. In the reviewed short-height viewports, the control obscured essential gameplay elements while the FRAME implementation kept them visible.

The control sizes cars from canvas **width** (`carWidth = roadWidth * 0.22`, height `× 2.12` in `createLayout`) and places the player with `playerY = height - carHeight - bottomPad`. That padding does not reserve the on-screen control bar. On a short stage the cars stay large, the player sits under Left/Right, and oncoming traffic is clipped by the HUD.

The FRAME run keeps a fixed 360×640 world (`PLAYER_Y = 452`) and scales it to the canvas. In the matching short-height capture the player sits fully above the buttons and oncoming traffic remains on screen. The control bar overlays the road, but it does not hide the car the player is driving. Visibility of those elements was observed; sufficient reaction time at those sizes was not measured.

Reviewed viewports:

| Capture | Size |
| --- | --- |
| Reviewer desktop window / stage | 1905×1312 window, 430×860 stage |
| Reviewer emulated mobile | 390×844 |
| Requester short-height screenshots | Control 431×461, FRAME 428×478 (game-stage crops; CSS viewport unrecorded) |

## Scorecard

| Parameter | Control (no FRAME) | FRAME |
| --- | --- | --- |
| Functionality | 29 / 40 | 36 / 40 |
| Code quality | 23 / 30 | 26 / 30 |
| Visuals and usability | 16 / 30 | 27 / 30 |
| Short-height play | Player under controls, traffic clipped | Player and traffic remain visible |
| Pause while holding P / Esc | Toggles pause and resume on key-repeat | Stays paused (`event.repeat` ignored) |
| Player vs oncoming cars | Player sprite much thinner than enemies; headlight is a disconnected triangle | Shared body, cabin, and lamp drawing |
| Obstacle fairness | Opposite-lane gap from current speed | Opposite-lane gap from max speed |
| `npm test` / `npm run build` | 13 tests pass; build passes | 19 tests pass; build passes |
| Best score across reload | Verified | Verified |
| Reported token consumption, including helpers | ~4M | ~5.6M |
| Recommendation | Drop | Keep |
| **Total** | **68 / 100** | **89 / 100** |

The initial review scored the control 81/100 and FRAME 88/100. After receiving additional UI screenshots and a request to reassess the implementations using that evidence, the reviewer revised the scores to 68 and 89. The requester did not prescribe a score adjustment.

## Reading the results

**Both runs.** Each shipped a client-only Vue 3 + TypeScript + Vite mini-game with two lanes, oncoming cars, score, start / crash / restart, pause that can freeze a run, on-screen lane buttons, keyboard left/right and pause, difficulty that increases over time, a README, and `npm run dev` / `build`. Both persisted a best score across reload; weaker runs did not overwrite it. Browser checks covered collisions, pause freeze, several restarts, and keyboard and touch-button lane changes.

**Visual trade-offs.** On the tall 430×860 stage the control uses photo sprites, grass stripes, a crash tumble, and near-miss `+40` floaters; the FRAME run uses vector cars. WebAudio cues exist in the control source; they were not verified by ear. These are style differences, not a reason to prefer the control once short-height occlusion, pause-repeat, and the player/headlight drawing are counted as defects.

**Where the FRAME run was stronger.** In the reviewed short-height captures, essential elements stayed visible. Pause ignored key-repeat. Opposite-lane gaps are sized at maximum speed so a pair that was dodgeable at the start stays dodgeable later by that metric. Collision and fairness are named in tests (`placeEnemy`, trapping pairs over 4000 steps) rather than only implied by waiting until crash. Cars share one geometry, so the player does not shrink relative to traffic. A `localStorage` try/catch is present in the FRAME source; behaviour with storage blocked was not tested. Tab-hide pause is present in source; it was not exercised in the browser pass.

**Where the FRAME run was weaker.** Independent `scaleX` / `scaleY` from a 360×640 world onto a taller stage stretches the scene slightly. Touch buttons bind both `pointerdown` and `click`; no resulting defect was observed. There is no crash-tumble cinema comparable to the control.

**Requester judgement.** After the short-height screenshots, the person who asked for the product preferred the FRAME run and chose to drop the control. That matches the revised scored recommendation.

**Remaining limitation.** No physical phone was used. Pause-overlay Restart was code-reviewed rather than clicked. Long fairness at top speed was taken from unit simulations (control 2400 frames, FRAME 4000), not a full live run.

FRAME produced the stronger implementation in this comparison, at approximately 40% higher reported token consumption. The cost of bringing the control implementation to an acceptable state was not measured.
