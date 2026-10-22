---
name: ai-sdlc-2-design
description: Plan the minimal components, applicable security/privacy checks and the test plan for the current use case. Use after a UC is specified and before writing code.
---

# Phase 2 — Design

## Goal
The smallest secure design that satisfies every AC, recorded in the UC itself.

## Steps
1. Read the current UC, plus the Architecture and Risk Tier sections of `docs/PROJECT.md`.
2. Search the codebase for components you can reuse or extend.
3. Fill the UC's **Design** section: the components per layer, plus the files to create or change.
4. Fill the UC's **Checklist** section with the items from `docs/CHECKLIST.md` that this UC touches, for every tier up to the project's tier. A new data flow or provider:
   - adds a row to the privacy table in `PROJECT.md`
   - may raise the risk tier; if so, ask the user
5. Fill the **Test Plan**: map every AC and every testable checklist item to the lowest test level that can prove it.
   - logic → unit
   - boundaries (API, data, webhooks) → integration
   - user journeys, UI, headers, accessibility → e2e
6. Update `docs/PROJECT.md` only if the architecture, tier or processors change.

## Rules
- Respect the dependency rule in `PROJECT.md`.
- Prefer hosted, proven services for auth, payments and email over custom code.
- No speculative abstractions. Build only what the ACs require.
- If there is a real trade-off, present the options to the user and recommend one.

## Exit
UC `Status: designed`, with every AC and checklist item mapped to a test or a manual check. Set `PHASE: 3`.
