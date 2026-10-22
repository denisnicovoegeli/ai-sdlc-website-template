---
name: ai-sdlc-4-validate
description: Verify the whole repository is release-ready, covering checks, the UC acceptance criteria and CI. Use after development, before deploying.
---

# Phase 4 — Validate

## Goal
Evidence that the UC works and nothing else broke.

## Steps
1. **Run** every command in `docs/PROJECT.md`: lint, typecheck, test, E2E, build.
2. **Trace**: tick each AC in the UC and name the test that proves it.
3. **Review** the diff for security issues (input validation, secrets, auth), accessibility and obvious performance problems.
4. **CI**: make sure `.github/workflows/ci.yml` runs lint, typecheck, test, E2E and build on every pull request. Create it only if it is missing.

## Rules
- Report results as they are; never weaken or skip a test to get green.
- On failure: if it is a spec gap, go back to Phase 1; if it is a bug, go back to Phase 3.

## Exit
Every check passes and every AC is ticked. UC `Status: done`. Set `PHASE: 5`.
