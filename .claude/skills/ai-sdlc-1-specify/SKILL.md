---
name: ai-sdlc-1-specify
description: Turn a feature or page request into a minimal use-case spec with testable acceptance criteria. Use when starting a new feature or page, or when validation shows a requirement gap.
---

# Phase 1 — Specify

## Goal
One UC file in `docs/specs/` whose acceptance criteria can be tested directly.

## Steps
1. **Find**: if a UC in `docs/specs/` already covers the request, update it. Otherwise copy `UC-TEMPLATE.md` to `UC-NNN-NAME.md`, where NNN is the next number and NAME is in UPPER-KEBAB case.
2. **Type**:
   - `feature` for behaviour (forms, booking, login)
   - `page` for content (About, Prices, Team)
3. **Clarify**: ask the user about actors, scope, content source, languages, edge cases and anything out of scope. Batch all questions into one message.
4. **Write** Intent, Flow, Edge Cases, Acceptance Criteria, and SEO & Languages:
   - each AC is Given/When/Then, observable, and has a unique ID
   - a page needs at least these ACs: the content renders in every language, the metadata is present, and it passes the accessibility and Lighthouse gates
5. **Confirm** the ACs with the user.

## Rules
- Describe behaviour, not implementation.
- Do not invent requirements or content; anything unclear is a question for the user.
- No code or tests in this phase.

## Exit
On a new branch `uc-NNN-name` from an up-to-date `main`, the UC is committed with `Status: specified`.
