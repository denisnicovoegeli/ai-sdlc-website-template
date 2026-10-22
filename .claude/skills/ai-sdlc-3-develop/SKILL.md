---
name: ai-sdlc-3-develop
description: Implement the current use case test-first, following its test plan. Use when a UC is designed and ready to build.
---

# Phase 3 — Develop

## Goal
Every AC from the UC is implemented and covered by a passing test.

## Loop (per AC, following the Test Plan)
1. **Red**: write the test and run it. It must fail for the expected reason.
2. **Green**: write the minimal code that makes it pass.
3. **Refactor**: clean up while the tests stay green.

For pure visual or layout work, implement it first and then cover it with an E2E or acceptance check.

## Rules
- Use only the commands in `docs/PROJECT.md`.
- Extend existing tests and code before creating new files.
- Test behaviour, not implementation details. No snapshot-only tests for logic.
- No features beyond the ACs. No dead code. Comment only where intent is non-obvious.
- Run lint and typecheck before you finish.
- If an AC turns out to be wrong or incomplete, stop and go back to Phase 1.

## Exit
All UC tests pass, and lint and typecheck are clean. Set `PHASE: 4`.
