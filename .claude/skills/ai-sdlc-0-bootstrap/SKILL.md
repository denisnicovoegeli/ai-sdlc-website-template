---
name: ai-sdlc-0-bootstrap
description: Set up or align a repository for AI-SDLC by choosing the stack, scaffolding it, wiring CI quality gates, protecting main and completing docs/PROJECT.md. Use for new repos, or when PROJECT.md has unknowns (tbd).
---

# Phase 0 — Bootstrap

## Goal
A runnable skeleton with every quality gate enforced in CI, a protected `main`, and `docs/PROJECT.md` fully filled in.

## Prerequisites
`git`, `gh` (logged in), the runtime, and the Vercel CLI. If any of them is missing, tell the user how to install it and stop.

## Steps
1. **Inspect** the existing structure, manifests, tests and CI. Reuse whatever fits.
2. **Clarify** with the user anything not already decided: purpose, risk tier, framework, package manager, site languages, CMS, booking, payment and email providers.
3. **Branch** `chore/bootstrap`. All the work below happens there.
4. **Scaffold** with the framework's official generator, if it has one. Add only what is missing:
   - lint, format, typecheck, unit and E2E tooling, plus axe
   - security headers in the **framework config** (not `vercel.json`), so local builds and CI test the same headers that production serves
   - i18n, if there is more than one language
   - a Lighthouse CI config with the budgets from `PROJECT.md`
   - smoke tests: one unit test, plus one E2E test that checks the headers and runs axe
   - external services (email, CMS, booking, payments) behind interfaces, mocked in CI
   - `.env.example` with env var names only
   - the Vercel function region set to `fra1`, unless the user wants otherwise
5. **CI**: `.github/workflows/ci.yml`
   - runs on pull requests and on pushes to `main`
   - `permissions: contents: read`; third-party actions are pinned to a commit SHA
   - installs from the lock file only (frozen install)
   - runs every gate in `PROJECT.md`, one job per gate, with stable job names
6. **Dependabot**:
   - `.github/dependabot.yml`: weekly and grouped, for the package ecosystem and GitHub Actions
   - `.github/workflows/dependabot-automerge.yml`: auto-merge patch and minor updates (`gh pr merge --auto --squash`); majors stay for manual review
7. **Document** the stack, risk tier, languages, architecture, commands and processors in `docs/PROJECT.md`. Replace `README.md` with a short project README (purpose, setup, commands).
8. **Verify** that every command passes locally. Then open a PR and wait for CI to go green on GitHub.
9. **Configure GitHub**, after the user confirms:
   - merge the bootstrap PR
   - repo settings: allow auto-merge, delete branches after merge, squash merge only
   - secret scanning and push protection on
   - branch protection on `main` (`gh api -X PUT repos/{owner}/{repo}/branches/main/protection --input -`):
     ```json
     {
       "required_status_checks": { "strict": true, "contexts": ["<every CI job name>"] },
       "enforce_admins": true,
       "required_pull_request_reviews": { "required_approving_review_count": 0 },
       "restrictions": null,
       "allow_force_pushes": false,
       "allow_deletions": false
     }
     ```
     `required_approving_review_count` must be `0`: you cannot approve your own PR, so any higher number locks you out. Private repos on GitHub Free do not support branch protection; if that applies, tell the user and stop.
10. **Vercel**: link the project, enable the Git integration, set the production branch to `main`, and set the env vars for preview and production.

## Rules
- Use stable, current versions. Lock files are committed.
- Ask before deleting or restructuring existing files.

## Exit
All gates are green in CI, `main` is protected, and the first preview deployment works.
