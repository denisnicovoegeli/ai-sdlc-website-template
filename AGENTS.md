# AGENTS.md — AI-SDLC Router

## Context (load in order)
1. `docs/TASKS.md` — current phase and use case (source of truth)
2. `docs/PROJECT.md` — stack, architecture, commands, deployment
3. Current UC — `docs/specs/UC-NNN-NAME.md`
4. Phase skill — `.claude/skills/ai-sdlc-<phase>-*/SKILL.md`

## Phases
| # | Phase     | Skill                  | Exit criteria                               |
|---|-----------|------------------------|---------------------------------------------|
| 0 | Bootstrap | `ai-sdlc-0-bootstrap`  | Stack chosen, `PROJECT.md` complete         |
| 1 | Specify   | `ai-sdlc-1-specify`    | UC with testable acceptance criteria        |
| 2 | Design    | `ai-sdlc-2-design`     | Components and test plan listed in UC       |
| 3 | Develop   | `ai-sdlc-3-develop`    | Acceptance criteria covered, tests green    |
| 4 | Validate  | `ai-sdlc-4-validate`   | Lint, types, tests, build and CI green      |
| 5 | Deploy    | `ai-sdlc-5-deploy`     | Released and smoke-checked                  |

Default flow: 1 → 2 → 3 → 4 → 5. A failing phase goes back to 1 (spec gap) or 3 (bug).

## Core Rules
- **Commands**: use only those in `docs/PROJECT.md`; never assume a toolchain.
- **Tests first**: write a failing test for every behaviour change, then implement (RED → GREEN → REFACTOR). Pure visual/layout work is covered by E2E or acceptance checks instead.
- **Architecture**: follow `docs/PROJECT.md`. Dependencies point inward; business logic stays free of framework, UI and I/O code.
- **Vertical slices**: one UC at a time, finished end to end before the next one starts.
- **Minimal artifacts**: edit existing files before creating new ones; no speculative features; no duplicates.
- **Secrets**: never commit them; reference platform env vars instead.
- **Language**: all generated content is in English.

## TASKS.md
Agents may update only `PHASE` and `Current Use Case`. The backlog belongs to the user.

## Stop and ask when
- requirements are ambiguous or conflict
- a dependency, credential or decision is missing
- an action is destructive or outward-facing (deleting files, deploying to production)

Do not guess.
