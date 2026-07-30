---
name: Quote and activate a group policy
description: Run the employer-side benefits setup — create a group, add employees, request quotes
  through a group quote intent, then establish the group policy through a group policy intent.
api: openapi/kota-openapi-original.json
base_url: https://api.kota.io
test_base_url: https://test.api.kota.io
operations:
  - CreateGroup
  - ListGroups
  - RetrieveGroup
  - UpdateGroup
  - AddEmployeeToGroup
  - ListGroupEmployees
  - CreateGroupQuoteIntent
  - ListGroupQuoteIntentRequirements
  - RetrieveGroupQuoteIntent
  - GetGroupQuoteIntentQuote
  - RejectGroupQuoteIntent
  - CreateGroupPolicyIntent
  - ListGroupPolicyIntentRequirements
  - RetrieveGroupPolicyIntent
  - ListGroupPolicies
  - RetrieveGroupPolicy
---

# Quote and activate a group policy

This is the employer-level half of a Kota integration: turn an employer plus a set of employees
into an active group policy with a benefits provider.

## The intent pattern

Kota models every mutating workflow the same way:

1. **Create** the intent.
2. **Fulfil its data requirements** — the intent returns dynamic required fields with their
   schemas. Collect them in your UI and submit them back. Answers can be submitted incrementally;
   the API keeps reporting what is still outstanding.
3. **Complete** — once requirements are satisfied the intent finalises and produces its result
   object.

Do not hard-code the requirement set. It varies by country, provider and product.

## Steps

1. **Ensure employer and employee data is synced.** See the
   `Sync employers and employees to Kota` skill. The employer must be `active`.
2. **Create the group.** Call `CreateGroup`. A group is the unified interface for one benefit or a
   predefined **bundle** (for example health insurance plus life assurance where a country requires
   them together). Bundles cannot be split — act on the whole group as a unit. Use multiple groups
   when the employer offers different plans to different employee segments.
3. **Add eligible employees.** Call `AddEmployeeToGroup` for each. Verify membership with
   `ListGroupEmployees`.
4. **Request quotes.** Call `CreateGroupQuoteIntent`. Create more than one to compare providers.
5. **Fulfil quote requirements.** Call `ListGroupQuoteIntentRequirements` and render the returned
   fields. Submit answers, then re-check until nothing is outstanding. Poll
   `RetrieveGroupQuoteIntent` or listen for `employer.health_insurance.quote.action_required`.
6. **Read the quote.** Call `GetGroupQuoteIntentQuote` for pricing, coverage detail and terms.
   Present it to the employer verbatim — use Kota's own wording so you do not step into regulated
   insurance-sales language.
7. **Decline unwanted quotes.** Call `RejectGroupQuoteIntent`.
8. **Establish the policy.** Once a quote is chosen, call `CreateGroupPolicyIntent`, then fulfil
   `ListGroupPolicyIntentRequirements` the same way and confirm via `RetrieveGroupPolicyIntent`.
9. **Read the resulting group policy.** Call `RetrieveGroupPolicy` (or `ListGroupPolicies`) for
   coverage terms, start and renewal dates, enrolled employees and premium structure. This is the
   master contract; individual employee policies derive from it.

## Simplified and migration flows

- **Simplified flow** — where quoting happened off-platform, Kota pre-creates the group and group
  policy. Skip to `ListGroups` and `AddEmployeeToGroup`.
- **Migration** — existing benefits are brought over with a policy import intent
  (`CreatePolicyImportIntent`), and groups and group policies are created during that migration.

## Rules

- Send `Idempotency-Key: <uuid-v4>` on every POST; a mismatched replay returns
  `409 idempotency_error`.
- `400 invalid_state` means the resource's current status forbids the transition — re-read the
  resource rather than retrying.
- `500 third_party_error` means an insurer API failed, not your request. Retry later.
- Handle `employer.health_insurance.quote.action_required` promptly: it carries a `required_action`
  object with `reason`, `reason_description` and `due_at` that is time-sensitive for the employer.
