---
name: ai-sdlc-1-specify
description: Turn a feature request into a minimal use-case spec with testable acceptance criteria. Use when starting a new feature or when validation shows a requirement gap.
---

# Phase 1 — Specify

## Goal
One UC file in `docs/specs/` whose acceptance criteria can be tested directly.

## Steps
1. **Find**: if a UC in `docs/specs/` already covers the feature, update it. Otherwise copy `UC-TEMPLATE.md` to `UC-NNN-NAME.md`, where NNN is the next number and NAME is in UPPER-KEBAB case.
2. **Clarify**: ask the user about actors, scope, edge cases and anything out of scope. Batch all questions into one message.
3. **Write** Intent, Preconditions, Flow, Edge Cases and Acceptance Criteria:
   - each AC is Given/When/Then, observable, and has a unique ID
   - add Non-Functional only if it matters for this UC
4. **Confirm** the ACs with the user.

## Rules
- Describe behaviour, not implementation.
- Do not invent requirements; anything unclear is a question for the user.
- No code or tests in this phase.

## Exit
UC `Status: specified`. In `docs/TASKS.md`, set `Current Use Case` and `PHASE: 2`.
