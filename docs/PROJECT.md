# PROJECT.md

## Purpose
_One or two sentences: what the system does and for whom._

## Risk Tier
_1 | 2 | 3_ — see `docs/CHECKLIST.md`
- 1: content pages + contact form
- 2: + CMS, booking or other third-party data flows
- 3: + login, personal accounts or payments

## Stack
- Language / framework: _tbd_
- Package manager: _tbd_
- CMS / booking / payments: _tbd or none_
- Email: _tbd_
- Hosting: Vercel (function region `fra1`)

## Languages
- Site content: _e.g. de-CH (default), fr-CH_
- With more than one language: i18n is set up from the start (localized routes, `hreflang`, translated metadata).

## Architecture
_Style (e.g. feature folders, hexagonal) and the dependency rule between layers._

## Structure
_Top-level directories and what belongs in each._

## Commands
| Task       | Command |
|------------|---------|
| Install    | _tbd_   |
| Dev        | _tbd_   |
| Lint       | _tbd_   |
| Typecheck  | _tbd_   |
| Test       | _tbd_   |
| E2E        | _tbd_   |
| Build      | _tbd_   |
| Lighthouse | _tbd_   |
| Audit      | _tbd_   |

## Quality Gates (CI, required to merge)
| Gate             | Threshold |
|------------------|-----------|
| Lint, typecheck  | no errors |
| Unit + E2E tests | all pass |
| Accessibility    | WCAG 2.2 AA; axe in E2E: 0 serious or critical violations |
| Security headers | E2E test asserts the headers from `CHECKLIST.md` (set in the framework config) |
| Dependencies     | audit: no high or critical; Dependabot enabled |
| Lighthouse       | Performance ≥ 90 · Accessibility ≥ 95 · Best Practices ≥ 95 · SEO ≥ 95 |
| Core Web Vitals  | LCP ≤ 2.5 s · CLS ≤ 0.1 · TBT ≤ 200 ms |

Lighthouse runs in CI against a local production build: mobile profile, median of 3 runs. Pages: home, contact, and one page per template.

### Exceptions
| Page | Gate | Threshold | Reason |
|------|------|-----------|--------|
| _e.g. /booking_ | _Performance_ | _≥ 75_ | _unavoidable third-party widget_ |

## Privacy (Swiss revDSG)
| Processor | Purpose | Data | Location |
|-----------|---------|------|----------|
| Vercel    | Hosting | IP, request logs | _region_ |

## Deployment
- Preview: every pull request (Vercel Git integration)
- Production: squash-merge to protected `main` after CI passes (0 approvals required, admins included)
- Dependencies: Dependabot weekly; patch and minor updates auto-merge when CI is green
- Env vars: managed in Vercel; listed (names only) in `.env.example`
- Monitoring: _uptime monitor, error tracking_
