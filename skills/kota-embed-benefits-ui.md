---
name: Embed the Kota benefits UI
description: Issue a short-lived Embed session token from your backend and mount Kota's prebuilt
  employer or employee benefits UI into your product, or hand off to a Kota-hosted session.
api: openapi/kota-openapi-original.json
base_url: https://api.kota.io
test_base_url: https://test.api.kota.io
operations:
  - CreateEmbedSession
  - CreateHostedSession
  - RetrieveEmployer
  - RetrieveEmployee
---

# Embed the Kota benefits UI

Use this when you want Kota's compliant benefits experience inside your product without building
the quoting and enrolment flows yourself. Kota owns the regulated insurance-sales language inside
these surfaces, which is why the loader must come from Kota's CDN.

## Embed (mount into your page)

1. **Sync the employer and employee first** — the embedded UI renders their real state.
2. **Issue a session token server-side.** Call `CreateEmbedSession` from your backend with your
   secret API key. Never expose the API key to the browser. The response carries an access token
   scoped to either an employer or an employee context; your backend must track which.
3. **Load Kota.js from Kota's CDN.** Production `https://js.kota.io/v1`, test
   `https://test.js.kota.io/v1`. Do not bundle it or self-host it — the docs require direct loading
   so compliance updates apply automatically. Confirm production is not loading the test SDK.
4. **Mount the UI.**
   - Employer: `Kota.Health.employer()` then `.init(employerAccessToken, { container, theme })`.
     Defaults to a `<div id="employer">`. The `dependants_cover` option (`full` | `binary` | `none`)
     controls whether the employer can cover spouse and children separately, all-or-none, or not
     at all.
   - Employee: `Kota.Health.employee()` then `.init(employeeAccessToken, { container, theme })`.
     Defaults to a `<div id="employee">`.
5. **Theme it** with `primaryColor`, `backgroundColor`, `radius` and `ringColor`.
6. **Listen for browser events** — this is the only browser-side channel. Either
   `employerEmbed.on('pageLoaded', handler)` or
   `window.addEventListener('employer.pageLoaded', handler)`. Available events:
   `pageLoaded` (carries `pageTitle`), `healthSetupLoaded`, `healthManagementLoaded` and
   `loadError`, each namespaced `employer.` or `employee.` on the window.
7. **Always handle `loadError`** and render your own fallback.

## Hosted (redirect instead of mount)

Call `CreateHostedSession` to get a one-off link into the fully Kota-hosted experience. Lowest
integration effort; theming is supported but there is no in-page mounting.

## Rules

- Send `Idempotency-Key: <uuid-v4>` on both `CreateEmbedSession` and `CreateHostedSession`.
- Session tokens are short-lived and context-bound. Mint a fresh one per user session rather than
  caching; do not reuse an employer token for an employee UI.
- Server-side state changes still arrive by webhook, not by browser event. Browser events are for
  your own metrics and UI reactions only — see `asyncapi/kota-webhooks.yml` for the source of
  truth.
