---
name: ai-sdlc-5-deploy
description: Release the validated use case to the hosting platform defined in docs/PROJECT.md and smoke-check it.
disable-model-invocation: true
---

# Phase 5 — Deploy

## Goal
The validated change is live and verified.

## Steps
1. **Check setup**: the platform and project link, build settings and required env vars from `docs/PROJECT.md` and `.env.example`. If anything is missing, ask the user.
2. **Preview**: open a pull request, then smoke-test its preview deployment against the UC's ACs.
3. **Production**: merge or promote only after the user confirms.
4. **Verify**: smoke-test production (key pages load, no console or server errors).
5. **Rollback**: if verification fails, roll back to the previous deployment and go back to Phase 1.

## Rules
- Never commit secrets; set them in the platform.
- Never deploy to production without explicit confirmation.

## Exit
Production is verified. Move the UC to done in the backlog and set `PHASE: 1` for the next UC.
