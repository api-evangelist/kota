---
name: Sync employers and employees to Kota
description: Create and keep in sync the employer legal entities and employee records that every
  Kota benefits flow depends on, including offboarding and its cancellation.
api: openapi/kota-openapi-original.json
base_url: https://api.kota.io
test_base_url: https://test.api.kota.io
operations:
  - CreateEmployer
  - ListEmployers
  - RetrieveEmployer
  - UpdateEmployer
  - OffboardEmployer
  - CreateEmployee
  - ListEmployees
  - RetrieveEmployee
  - UpdateEmployee
  - OffboardEmployee
  - CancelOffboardingEmployee
---

# Sync employers and employees to Kota

Every Kota benefits flow — quoting, group setup, enrolment, contribution reporting — reads from
employer and employee records. Sync them first and keep them current.

## Before you start

- Authenticate with `Authorization: Bearer <API_SECRET_KEY>`. Test keys are prefixed `pk_test_`
  and target `https://test.api.kota.io`; live keys are prefixed `pk_live_` and target
  `https://api.kota.io`.
- Your key is bound to one platform and to that platform's type (for example
  `employer_of_record` or `payroll_provider`). Some operations are restricted by type and return
  `403 forbidden` when they are not available to you.
- Send `Idempotency-Key: <uuid-v4>` on every POST. See `conventions/kota-conventions.yml`.

## Steps

1. **Create the employer.** Call `CreateEmployer` for each legal entity, one per country. A new
   employer starts in `pending` while Kota runs regulatory checks and moves to `active` when it is
   ready for a group policy. Create employers early so they are active by the time you need them.
2. **Poll or listen for activation.** Either call `RetrieveEmployer` and check `status`, or handle
   the `employer.created` / `employer.updated` webhooks (see `asyncapi/kota-webhooks.yml`). Do not
   attempt group setup while the employer is `pending`.
3. **Create employees.** Call `CreateEmployee` for each individual who may receive benefits.
   Employees also start `pending` and become `active` once processed.
4. **Keep records current.** Push changes with `UpdateEmployer` and `UpdateEmployee`. Use
   `ListEmployers` and `ListEmployees` to reconcile; both paginate with `page` and `page_size` and
   return `items`, `page`, `page_size`, `total_count`.
5. **Offboard on termination.** Call `OffboardEmployee` when someone leaves, and `OffboardEmployer`
   when an entity stops offering benefits. Offboarding is scheduled, not instant.
6. **Reverse a mistaken offboarding.** Call `CancelOffboardingEmployee`. This only works while the
   offboarding is still pending; otherwise Kota returns `400 invalid_state` with a `detail`
   explaining why.

## Rules

- Retry only on `429 rate_limit_exceeded` and `5xx`, with exponential backoff. Never retry other
  `4xx` responses — the request will fail identically.
- Errors are RFC 9457 problem documents (`application/problem+json`) with `error_code` and
  `trace_id`. On `400 invalid_request`, read the `errors` object: it maps the JSON path of each
  invalid field to its error messages. Quote `trace_id` when contacting Kota support.
- Reusing an `Idempotency-Key` with different parameters returns `409 idempotency_error`. Keys are
  scoped to your token, are at most 200 characters, and expire after 1 hour.
- Never send an `Idempotency-Key` on GET, PUT or DELETE — it has no effect.
