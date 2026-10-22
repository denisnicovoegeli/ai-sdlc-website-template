---
name: ai-sdlc-2-design
description: Plan the minimal components and the test plan for the current use case. Use after a UC is specified and before writing code.
---

# Phase 2 — Design

## Goal
The smallest design that satisfies every AC, recorded in the UC itself.

## Steps
1. Read the current UC and the Architecture section of `docs/PROJECT.md`.
2. Search the codebase for components you can reuse or extend.
3. Fill the UC's **Design** section: the components per layer, plus the files to create or change.
4. Fill the **Test Plan**: map every AC to the lowest test level that can prove it.
   - logic → unit
   - boundaries (API, data, external services) → integration
   - user journeys and UI → e2e
5. Update `docs/PROJECT.md` only if the architecture itself changes.

## Rules
- Respect the dependency rule in `PROJECT.md`.
- No speculative abstractions. Build only what the ACs require.
- If there is a real trade-off, present the options to the user and recommend one.

## Exit
UC `Status: designed`, with every AC mapped to a test. Set `PHASE: 3`.
