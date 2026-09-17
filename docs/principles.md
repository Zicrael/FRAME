# Principles

FRAME is guided by five engineering principles. They define how problems should be approached, decisions made, solutions implemented, and results evaluated.

---

## Consideration Before Implementation

*Think before you build.*

Every implementation should begin with an understanding of the requested outcome and a considered approach. The depth of consideration should match the uncertainty and risk of the change, not the apparent importance of the request. If implementation reveals new information, the approach should be reconsidered.

---

## AI Assists, Engineers Decide

*Keep decisions explicit.*

AI can help investigate problems, propose alternatives, compare trade-offs, implement solutions, and evaluate results. It should support engineering judgment rather than replace it. The reasoning behind consequential decisions should remain explicit and understandable, so that an engineer can assess a decision instead of being asked to approve each step of the work. Ordinary engineering choices are resolved within the authority the request grants; missing authority, contradictory requirements, and unavailable information belong to the engineer.

---

## Respect the Existing System

*Understand before you change.*

Before making a change, understand how the relevant part of the existing system works, how it fits into the broader architecture, and which constraints shaped it. A solution should integrate with the existing system rather than treat the task in isolation.

---

## Simplicity Over Complexity

*Keep the solution simple.*

Prefer the simplest solution that satisfies the requirements and fits the existing system. Avoid unnecessary abstractions, duplicated logic, and complexity without a clear benefit.

---

## Validate Before You Trust

*Prove that it works.*

A solution should not be accepted because it looks convincing. Validate it against the original request, its requirements, and its constraints — including required work that may have been left out, not only behaviour that visibly broke. Validation should rely on evidence such as tests, execution, inspection, and observed behavior, and should say what it did not cover.
