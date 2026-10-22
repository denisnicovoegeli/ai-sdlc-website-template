---
name: ai-sdlc-4-validate
description: Verify the change is release-ready against all quality gates, the UC acceptance criteria and the security/privacy checklist. Use after development, before deploying.
---

# Phase 4 — Validate

## Goal
Evidence that the UC works, is secure and accessible, and that nothing else broke.

## Steps
1. **Gates**: run every command in `docs/PROJECT.md` locally. Every threshold must be met, or the page must be listed under Exceptions.
2. **Trace**: tick each AC and each item in the UC's Checklist section, and name the test or manual check that proves it.
3. **Manual accessibility check** on the changed pages:
   - the whole flow works with the keyboard alone
   - focus is visible
   - a quick screen-reader pass (NVDA or VoiceOver)
   - zoom to 200 % works
4. **Preview**: open the PR's Vercel preview and check the ACs there, including real integrations (email arrives, booking works).
5. **Review** the diff for:
   - injection, unvalidated input, permission checks and leaked secrets
   - personal data going to new processors not listed in `PROJECT.md`
   - CSP or header regressions
   - missing translations or metadata
6. **Finish**: set the UC to `Status: done`, commit, and mark the PR ready for review. The PR description contains a summary and the ticked AC list.

## Rules
- Report results as they are; never weaken a test, threshold or check to get green.
- An exception needs a written reason in `PROJECT.md` and the user's approval.
- On failure: if it is a spec gap, go back to Phase 1; if it is a bug, go back to Phase 3.

## Exit
The PR is ready, CI is green, and every AC and checklist item is ticked.
