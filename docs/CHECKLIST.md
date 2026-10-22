# CHECKLIST.md — Security, Privacy, SEO

Apply every tier up to and including the project's risk tier in `docs/PROJECT.md`.
In Phase 2, copy the items that apply into the UC. In Phase 4, tick them.

## Tier 1 — Content + contact form
**Security**
- [ ] Headers: `Content-Security-Policy` (no `unsafe-inline` scripts; nonces or hashes), `Strict-Transport-Security`, `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin`, `Permissions-Policy`, and `frame-ancestors 'none'` in the CSP
- [ ] All input is validated on the server against a schema; the client-side checks are only for UX
- [ ] Forms are protected by a honeypot and rate limiting; on serverless this needs a shared store or the platform firewall, since in-memory counters don't work. A captcha only if spam persists.
- [ ] Emails and messages built from user input are escaped; no header injection
- [ ] The email sending domain has SPF, DKIM and DMARC records
- [ ] No secrets or private API keys in the client bundle
- [ ] Dependencies come from lock files; Dependabot is on for packages and GitHub Actions

**Privacy (revDSG)**
- [ ] A privacy policy lists every processor from `PROJECT.md` and where it stores data
- [ ] The legal notice (Impressum) is linked from every page
- [ ] Forms collect only the data they need and state the purpose next to the form
- [ ] Third-party embeds (maps, video, social) load only on click (facade)
- [ ] Analytics are cookieless; anything that sets non-essential cookies waits for consent

**Accessibility (WCAG 2.2 AA)**
- [ ] axe passes; the manual keyboard, focus, screen-reader and 200 % zoom check is done
- [ ] Every form field has a label, and errors are announced and linked to their field

**SEO & quality**
- [ ] A unique `<title>` and meta description per page and language
- [ ] `sitemap.xml`, `robots.txt` and a canonical URL on every page; `hreflang` if there is more than one language
- [ ] `LocalBusiness` structured data (address, opening hours, contact)
- [ ] Images are optimized (modern formats, sized, lazy below the fold); fonts are self-hosted
- [ ] A custom 404 page

## Tier 2 — + CMS, booking, third-party data
- [ ] CMS users have the fewest permissions they need; editors cannot change code or settings
- [ ] CMS content is sanitized before it is rendered as HTML
- [ ] Webhooks verify their signature and reject replays
- [ ] Preview and draft modes need a secret token
- [ ] Booking data is minimal, with a retention period defined and documented
- [ ] Every new processor is added to the `PROJECT.md` privacy table

## Tier 3 — + login, accounts, payments
- [ ] Auth uses a proven library or provider; no custom crypto or session handling
- [ ] Sessions use cookies set as `HttpOnly`, `Secure` and `SameSite=Lax` (or stricter)
- [ ] Forms that change state are protected against cross-site request forgery (CSRF)
- [ ] Permissions are checked on the server for every request and every resource (no IDOR)
- [ ] Login and password reset are rate limited; error messages are generic
- [ ] Payments only go through hosted checkout (e.g. Stripe Checkout); card data never touches the site
- [ ] Payment webhooks are verified and idempotent; order state comes from the webhook, not from the redirect
- [ ] Users can view, export and delete their own data
- [ ] Security-relevant events are logged, without personal data or secrets in the logs
