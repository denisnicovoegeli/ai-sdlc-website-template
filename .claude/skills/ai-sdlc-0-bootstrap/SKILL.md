---
name: ai-sdlc-0-bootstrap
description: Set up or align a repository for AI-SDLC by choosing the stack, scaffolding it and completing docs/PROJECT.md. Use for new repos, or when PROJECT.md has unknowns (tbd).
---

# Phase 0 — Bootstrap

## Goal
A runnable, testable skeleton, with `docs/PROJECT.md` fully filled in.

## Steps
1. **Inspect** the existing structure, manifests, tests and CI. Reuse whatever fits.
2. **Clarify** with the user anything not already decided: purpose, language/framework, package manager, test runners (unit and E2E), hosting.
3. **Scaffold** with the framework's official generator, if it has one. Add only what is missing:
   - lint, format, typecheck and test tooling
   - one passing smoke test (unit) and one E2E test
   - `.env.example` with env var names only
4. **Document** stack, architecture, structure, commands and deployment in `docs/PROJECT.md`.
5. **Verify** that every command in `PROJECT.md` runs successfully.

## Rules
- Use stable, current versions. Lock files are committed.
- Ask before deleting or restructuring existing files.

## Exit
All `PROJECT.md` commands work. Set `PHASE: 1` in `docs/TASKS.md`.
