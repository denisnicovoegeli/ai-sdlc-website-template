---
name: ai-sdlc-4-validate
description: Verify the change is release-ready against all quality gates, the UC acceptance criteria and the security/privacy checklist. Use after development, before deploying.
---

# Phase 4 — Validate

## Goal
Evidence that the UC works, is secure, and that nothing else broke.

## Steps
1. **Gates**: run every command in `docs/PROJECT.md` locally (lint, typecheck, test, E2E with axe, build, Lighthouse, audit). Every threshold must be met, or the page must be listed under Exceptions.
2. **Trace**: tick each AC and each item in the UC's Checklist section, and name the test or manual check that proves it.
3. **Review** the diff for:
   - injection, unvalidated input, permission checks and leaked secrets
   - personal data going to new processors not listed in `PROJECT.md`
   - CSP or header regressions
   - accessibility, plus missing translations or metadata
4. **PR**: open or update the pull request for the UC branch, with a summary and the AC checklist. CI must be green.

## Rules
- Report results as they are; never weaken a test, threshold or check to get green.
- An exception needs a written reason in `PROJECT.md` and the user's approval.
- On failure: if it is a spec gap, go back to Phase 1; if it is a bug, go back to Phase 3.

## Exit
CI is green on the PR, and every AC and checklist item is ticked. UC `Status: done`. Set `PHASE: 5`.
