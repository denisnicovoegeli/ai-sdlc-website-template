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
   - the platform project is linked
   - the env vars in `.env.example` are set for preview and production
   - if anything is missing, ask the user
2. **Preview**: smoke-test the PR's preview deployment:
   - the UC's ACs
   - the response headers
   - forms end to end (the email arrives, spam is blocked)
3. **Production**: merge the PR only after the user confirms. The platform then deploys `main`.
4. **Verify** production:
   - key pages load in every language
   - no console or server errors
   - headers are present
   - `sitemap.xml` and `robots.txt` are correct
5. **Monitor**: an uptime check and error tracking are active. A new monitoring provider is a processor, so add it to `PROJECT.md`.
6. **Rollback**: if verification fails, roll back to the previous deployment (instant rollback on the platform) and go back to Phase 1.

## Rules
- Never commit secrets; set them on the platform.
- Never merge to `main` or deploy to production without explicit confirmation.

## Exit
Production is verified and monitored. Move the UC to done in the backlog and set `PHASE: 1` for the next UC.
