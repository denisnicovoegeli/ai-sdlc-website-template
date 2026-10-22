---
name: ai-sdlc-0-bootstrap
description: Set up or align a repository for AI-SDLC by choosing the stack, scaffolding it, wiring CI quality gates, protecting main and completing docs/PROJECT.md. Use for new repos, or when PROJECT.md has unknowns (tbd).
---

# Phase 0 — Bootstrap

## Goal
A runnable skeleton with every quality gate enforced in CI, and `docs/PROJECT.md` fully filled in.

## Steps
1. **Inspect** the existing structure, manifests, tests and CI. Reuse whatever fits.
2. **Clarify** with the user anything not already decided: purpose, risk tier, framework, package manager, site languages, CMS, booking and payment providers, hosting.
3. **Scaffold** with the framework's official generator, if it has one. Add only what is missing:
   - lint, format, typecheck, unit and E2E tooling, plus axe
   - security headers in the framework or hosting config, following `docs/CHECKLIST.md`
   - i18n, if there is more than one language
   - a Lighthouse CI config with the budgets from `PROJECT.md`
   - smoke tests: one unit test, plus one E2E test that checks the security headers and runs axe
   - `.env.example` with env var names only
4. **CI**: `.github/workflows/ci.yml` runs every gate in `PROJECT.md` on each pull request and push to `main`. `.github/dependabot.yml` covers both the package ecosystem and GitHub Actions.
5. **Document** the stack, risk tier, languages, architecture, commands and processors in `docs/PROJECT.md`.
6. **Verify** that every command passes locally and that CI is green on GitHub.
7. **Protect `main`** with `gh`, after the user confirms:
   ```bash
   gh api -X PUT repos/{owner}/{repo}/branches/main/protection --input protection.json
   ```
   Require a pull request, require the CI checks to pass with the branch up to date, block force pushes and deletion, and apply the rules to admins too. The check names must match jobs that have already run. Private repos on GitHub Free cannot use branch protection; if that applies, tell the user and stop.

## Rules
- Use stable, current versions. Lock files are committed.
- Ask before deleting or restructuring existing files.

## Exit
All gates are green in CI and `main` is protected. Set `PHASE: 1` in `docs/TASKS.md`.
