# Website Template — AI-SDLC

A spec-driven, test-first workflow for small-business websites, built for AI coding agents.
It is stack-agnostic and ships on Vercel by default.

## Start a new project
1. Create a repo from this template (`gh repo create <name> --template <owner>/website-template --public --clone`).
2. Install the prerequisites: Git, GitHub CLI (`gh auth login`), Node.js or your runtime, and the Vercel CLI.
3. Run `/ai-sdlc-0-bootstrap` in Claude Code. It asks about the stack, risk tier and languages; scaffolds the app, CI and Dependabot; fills in `docs/PROJECT.md`; and protects `main`.
4. Add use cases to `docs/TASKS.md`, then run `/ai-sdlc-1-specify` for the first one.

## Workflow
Specify → Design → Develop → Validate → Deploy, one use case per branch and PR.
Small changes take the fast path: branch → PR → CI → merge.

| File | Purpose |
|------|---------|
| `AGENTS.md` | Rules and phase router for any agent |
| `docs/PROJECT.md` | Stack, risk tier, quality gates, commands, processors |
| `docs/CHECKLIST.md` | Security, privacy (revDSG) and SEO checks by risk tier |
| `docs/TASKS.md` | Backlog, owned by you |
| `docs/specs/` | One spec per use case or page |
| `.claude/skills/` | Phase instructions |
| `.claude/settings.json` | Blocks risky agent actions locally |

Bootstrap replaces this README with the project's own.
