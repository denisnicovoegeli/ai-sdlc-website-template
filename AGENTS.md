# AGENTS.md — AI-SDLC Router

## Source of Truth
- Repository state is defined in: `docs/TASKS.md`
- Agents MUST NOT modify this file
- All work MUST align with tasks defined there

---

## SDLC Phases
0. BOOTSTRAP  
1. SPECIFY  
2. DESIGN  
3. DEVELOP  
4. VALIDATE  
5. DEPLOY  

- Phases are non-linear and MAY be skipped or repeated

### Default Workflow
SPECIFY → DESIGN → DEVELOP → VALIDATE

### Iteration Loop
VALIDATE → SPECIFY

### Post-Deployment Feedback Loop
DEPLOY → SPECIFY

---

## Context Loading Order (STRICT)
Agents MUST load context in the following order:

1. `docs/TASKS.md`
2. `docs/PROJECT.md`
3. `docs/specs/UC-[NNN]-[NAME].md`
4. Phase-specific skill

Deviation from this order is NOT allowed.

---

## Phase → Skill Mapping

| Phase     | Skill                          |
|----------|--------------------------------|
| 0        | skills/ai-sdlc-0-bootstrap     |
| 1        | skills/ai-sdlc-1-specify       |
| 2        | skills/ai-sdlc-2-design        |
| 3        | skills/ai-sdlc-3-develop       |
| 4        | skills/ai-sdlc-4-validate      |
| 5        | skills/ai-sdlc-5-deploy        |

---

## Commands

### Run tests
```bash
pytest -q
```

### Build container
```bash
docker build -t app:local .
```

### Run container
```bash
docker run --rm -p 8000:8000 app:local
```

---

## Core Rules

### Language
- All generated content MUST be in English

### Artifact Management
- MODIFY existing artifacts whenever possible
- CREATE artifacts ONLY if they do not exist
- DO NOT duplicate artifacts
- KEEP artifacts minimal and focused

### Development Process (STRICT TDD)
1. Write failing tests
2. Implement code
3. Make tests pass

- Every change MUST be test-backed
- Code without tests is NOT allowed

---

## Architecture (MANDATORY)

Follow Clean Architecture strictly:

```
domain ← application ← interfaces ← infrastructure
```

### Rules
- Dependencies MUST point inward only
- Domain layer MUST remain framework-independent
- Infrastructure MUST NOT contain business logic
- Interfaces MUST NOT bypass application layer

---

## Delivery Strategy
- Implement SMALL vertical slices
- Each slice MUST deliver ONE complete Use Case (UC)
- DO NOT split a single UC across multiple incomplete implementations

---

## Phase Execution Rules

### 0 — BOOTSTRAP
- Initialize project structure
- Ensure tooling, environment, and dependencies are ready

---

### 1 — SPECIFY
- Define clear, testable requirements
- Produce or update UC specification
- If ANY ambiguity exists → STOP and ask the user

---

### 2 — DESIGN
- Produce minimal architecture required for the UC
- Avoid over-engineering
- Ensure design respects Clean Architecture

---

### 3 — DEVELOP
- Follow STRICT TDD
- Implement only what is required to pass tests
- Do not introduce speculative features

---

### 4 — VALIDATE
- Run all tests (`pytest -q`)
- Validate implementation against requirements
- If ANY test fails → return to SPECIFY

---

### 5 — DEPLOY
- Deploy ONLY if:
  - All tests pass
  - Requirements are satisfied
- Build and run container:
  ```bash
  docker build -t app:local .
  docker run --rm -p 8000:8000 app:local
  ```

---

## Failure Handling

If any of the following occur:
- Unclear or ambiguous requirements
- Conflicting specifications
- Missing dependencies
- Architectural uncertainty

→ IMMEDIATELY STOP  
→ ASK the user for clarification  

DO NOT guess  
DO NOT assume  

---

## Enforcement Priorities (Highest → Lowest)

1. `docs/TASKS.md`
2. Tests (TDD compliance)
3. Clean Architecture
4. Phase rules
5. Artifact minimality
