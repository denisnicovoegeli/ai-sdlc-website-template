---
name: ai-sdlc-5-deploy
description: Release the validated use case to the hosting platform defined in docs/PROJECT.md, smoke-check it and ensure monitoring.
disable-model-invocation: true
---

# Phase 5 — Deploy

## Goal
The validated change is live, verified and monitored.

## Steps
1. **Check setup**:
   - `main` is protected, with the CI checks required (`gh api repos/{owner}/{repo}/branches/main/protection`)
   - the env vars from `.env.example` are set for production
   - if anything is missing, ask the user
2. **First release only**:
   - custom domain added, with a `www` ↔ apex redirect and HTTPS working
   - email sending domain has SPF, DKIM and DMARC records
   - site verified in Google Search Console and `sitemap.xml` submitted
   - uptime monitor and error tracking set up (each provider added to the `PROJECT.md` privacy table)
3. **Merge** the PR after the user confirms (squash). The platform deploys `main` to production.
4. **Verify** production:
   - key pages load in every language
   - no console or server errors
   - headers are present
   - forms work end to end
   - `sitemap.xml` and `robots.txt` are correct
5. **Rollback**, if verification fails:
   1. Use the platform's instant rollback to the previous deployment. On Vercel this pauses automatic production deploys.
   2. Open a revert PR, and merge it once CI is green.
   3. Undo the rollback (re-enable automatic deploys), then reopen the UC at Phase 1 or 3.

## Rules
- Never commit secrets; set them on the platform.
- Never merge or deploy to production without explicit confirmation.

## Exit
Production is verified and monitored. Ask the user to move the UC to Done in `docs/TASKS.md`.
