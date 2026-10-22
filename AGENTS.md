# AGENTS.md — AI-SDLC Router

## Context (load in order)
1. `docs/TASKS.md` — current phase and use case (source of truth)
2. `docs/PROJECT.md` — stack, risk tier, quality gates, commands, deployment
3. Current UC — `docs/specs/UC-NNN-NAME.md`
4. Phase skill — `.claude/skills/ai-sdlc-<phase>-*/SKILL.md`
5. `docs/CHECKLIST.md` — in phases 2, 4 and 5

## Phases
| # | Phase     | Skill                  | Exit criteria                                     |
|---|-----------|------------------------|---------------------------------------------------|
| 0 | Bootstrap | `ai-sdlc-0-bootstrap`  | Stack chosen, CI gates green, `main` protected    |
| 1 | Specify   | `ai-sdlc-1-specify`    | UC with testable acceptance criteria              |
| 2 | Design    | `ai-sdlc-2-design`     | Components, test plan and checklist items in UC   |
| 3 | Develop   | `ai-sdlc-3-develop`    | Acceptance criteria covered, tests green          |
| 4 | Validate  | `ai-sdlc-4-validate`   | All quality gates and checklist items pass        |
| 5 | Deploy    | `ai-sdlc-5-deploy`     | Released, smoke-checked and monitored             |

Default flow: 1 → 2 → 3 → 4 → 5. A failing phase goes back to 1 (spec gap) or 3 (bug).

## Core Rules
- **Commands**: use only those in `docs/PROJECT.md`; never assume a toolchain.
- **Tests first**: write a failing test for every behaviour change, then implement (RED → GREEN → REFACTOR). Pure visual/layout work is covered by E2E or acceptance checks instead.
- **Architecture**: follow `docs/PROJECT.md`. Dependencies point inward; business logic stays free of framework, UI and I/O code.
- **Vertical slices**: one UC at a time, finished end to end before the next one starts.
- **Git**: one branch and one PR per UC (`uc-NNN-name`). Never commit to `main` directly; merge only when CI is green.
- **Security & privacy**: apply `docs/CHECKLIST.md` up to the project's risk tier. Never commit secrets; use platform env vars.
- **Minimal artifacts**: edit existing files before creating new ones; no speculative features; no duplicates.
- **Language**: docs, code, commits and specs are in English. Site content uses the languages listed in `docs/PROJECT.md`.

## Definition of Done
All quality gates in `docs/PROJECT.md` pass in CI, every AC is ticked, and the applicable checklist items are ticked.

## TASKS.md
Agents may update only `PHASE` and `Current Use Case`. The backlog belongs to the user.

## Stop and ask when
- requirements are ambiguous or conflict
- a dependency, credential or decision is missing
- an action is destructive or outward-facing (deleting files, changing repo settings, deploying to production)

Do not guess.
