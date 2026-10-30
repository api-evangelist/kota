# Kota

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Kota is a Dublin-headquartered employee benefits platform that gives payroll, HR and employer-of-record platforms embedded access to health insurance, workplace pensions, life assurance, flexible benefits and spend cards across Ireland, the UK, Spain and other markets. Kota Embedded is sold as three developer products — a Hosted redirect experience, an Embed JavaScript SDK (Kota.js) that drops themed employer and employee benefit UIs into a partner platform, and a full REST API for building a completely custom benefits journey. The Kota API is an OpenAPI 3.1 contract at api.kota.io covering employers, employees, groups, group policies, policies, plans, health insurance quotes and offers, contribution reports, associated persons/dependents, and a family of intent resources (group quote, group policy, enrolment, dependents management, policy amendment, policy import) that model each step of the benefits lifecycle. Authentication is API key bearer tokens with pk_test_/pk_live_ prefixes, POST requests accept an Idempotency-Key header, errors conform to RFC 9457 Problem Details, and a large webhook catalog (v1 and v2 event families) publishes employer, employee, group, policy, quote and contribution-report state changes.

**Areas:** Company · Fintech · Insurance · Employee Benefits · Health Insurance · Pensions · Insurtech · Embedded Finance · Human Resources · Payroll

## Kota on APIs.io

Everything profiled for Kota is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/kota/](https://apis.io/providers/kota/)** — or go straight to one of the APIs or properties below.

### APIs (24)

- [Kota Associated Persons API](https://apis.io/apis/kota/kota-associated-persons-api/) — The Associated Persons API from Kota — 2 operation(s) for associated persons.
- [Kota Contribution Reports API](https://apis.io/apis/kota/kota-contribution-reports-api/) — The Contribution Reports API from Kota — 5 operation(s) for contribution reports.
- [Kota Dependents Management Intents API](https://apis.io/apis/kota/kota-dependents-management-intents-api/) — The Dependents Management Intents API from Kota — 6 operation(s) for dependents management intents.
- [Kota Embed Sessions API](https://apis.io/apis/kota/kota-embed-sessions-api/) — The Embed Sessions API from Kota — 1 operation(s) for embed sessions.
- [Kota Employees API](https://apis.io/apis/kota/kota-employees-api/) — The employees API from Kota — 4 operation(s) for employees.
- [Kota Employers API](https://apis.io/apis/kota/kota-employers-api/) — The employers API from Kota — 3 operation(s) for employers.
- [Kota Enrolment Intents API](https://apis.io/apis/kota/kota-enrolment-intents-api/) — The Enrolment Intents API from Kota — 7 operation(s) for enrolment intents.
- [Kota Events API](https://apis.io/apis/kota/kota-events-api/) — The events API from Kota — 3 operation(s) for events.
- [Kota Group Policies API](https://apis.io/apis/kota/kota-group-policies-api/) — The Group Policies API from Kota — 2 operation(s) for group policies.
- [Kota Group Policy Intents API](https://apis.io/apis/kota/kota-group-policy-intents-api/) — The Group Policy Intents API from Kota — 3 operation(s) for group policy intents.
- [Kota Group Quote Intents API](https://apis.io/apis/kota/kota-group-quote-intents-api/) — The Group Quote Intents API from Kota — 5 operation(s) for group quote intents.
- [Kota Groups API](https://apis.io/apis/kota/kota-groups-api/) — The groups API from Kota — 4 operation(s) for groups.
- [Kota Health Insurance API](https://apis.io/apis/kota/kota-health-insurance-api/) — The Health Insurance API from Kota — 8 operation(s) for health insurance.
- [Kota Hosted Sessions API](https://apis.io/apis/kota/kota-hosted-sessions-api/) — The Hosted Sessions API from Kota — 1 operation(s) for hosted sessions.
- [Kota Plans API](https://apis.io/apis/kota/kota-plans-api/) — The plans API from Kota — 2 operation(s) for plans.
- [Kota Policies API](https://apis.io/apis/kota/kota-policies-api/) — The policies API from Kota — 2 operation(s) for policies.
- [Kota Policy Amendment Intents API](https://apis.io/apis/kota/kota-policy-amendment-intents-api/) — The Policy Amendment Intents API from Kota — 5 operation(s) for policy amendment intents.
- [Kota Policy Import Intents API](https://apis.io/apis/kota/kota-policy-import-intents-api/) — The Policy Import Intents API from Kota — 2 operation(s) for policy import intents.
- [Kota Providers API](https://apis.io/apis/kota/kota-providers-api/) — The providers API from Kota — 2 operation(s) for providers.
- [Kota Requirements API](https://apis.io/apis/kota/kota-requirements-api/) — The requirements API from Kota — 1 operation(s) for requirements.
- [Kota Webhooks API](https://apis.io/apis/kota/kota-webhooks-api/) — The webhooks API from Kota — 2 operation(s) for webhooks.
- [Kota API Reference API](https://apis.io/apis/kota/kota-api-reference-api/) — The API Reference API from Kota — 0 operation(s) for api reference.
- [Kota Types of events API](https://apis.io/apis/kota/kota-types-of-events-api/) — The Types of events API from Kota — 0 operation(s) for types of events.
- [Kota Types of events V2 API](https://apis.io/apis/kota/kota-types-of-events-v2-api/) — The Types of events V2 API from Kota — 0 operation(s) for types of events v2.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Kota Webhooks](https://apis.io/asyncapis/kota/kota-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [kota-docs](https://apis.io/servers/kota/kota-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Kota Agentic Access](https://apis.io/agentic-access/kota/kota-agentic-access/)

#### Collections (66)

Postman and Open Collection request collections.

- [API Reference Associated Persons API](https://apis.io/collections/kota/open-kota-associated-persons-api/)
- [API Reference Associated Persons associatedPersons API](https://apis.io/collections/kota/open-kota-associatedpersons-api/)
- [API Reference Associated Persons Contribution Reports API](https://apis.io/collections/kota/open-kota-contribution-reports-api/)
- [API Reference Associated Persons contributionReports API](https://apis.io/collections/kota/open-kota-contributionreports-api/)
- [API Reference Associated Persons Dependents Management Intents API](https://apis.io/collections/kota/open-kota-dependents-management-intents-api/)
- [API Reference Associated Persons dependentsManagementIntents API](https://apis.io/collections/kota/open-kota-dependentsmanagementintents-api/)
- [API Reference Associated Persons Embed Sessions API](https://apis.io/collections/kota/open-kota-embed-sessions-api/)
- [API Reference Associated Persons embedSessions API](https://apis.io/collections/kota/open-kota-embedsessions-api/)
- [API Reference Associated Persons employees API](https://apis.io/collections/kota/open-kota-employees-api/)
- [API Reference Associated Persons employers API](https://apis.io/collections/kota/open-kota-employers-api/)
- [API Reference Associated Persons Enrolment Intents API](https://apis.io/collections/kota/open-kota-enrolment-intents-api/)
- [API Reference Associated Persons enrolmentIntents API](https://apis.io/collections/kota/open-kota-enrolmentintents-api/)
- [API Reference Associated Persons events API](https://apis.io/collections/kota/open-kota-events-api/)
- [API Reference Associated Persons Group Policies API](https://apis.io/collections/kota/open-kota-group-policies-api/)
- [API Reference Associated Persons Group Policy Intents API](https://apis.io/collections/kota/open-kota-group-policy-intents-api/)
- [API Reference Associated Persons Group Quote Intents API](https://apis.io/collections/kota/open-kota-group-quote-intents-api/)
- [API Reference Associated Persons groupPolicies API](https://apis.io/collections/kota/open-kota-grouppolicies-api/)
- [API Reference Associated Persons groupPolicyIntents API](https://apis.io/collections/kota/open-kota-grouppolicyintents-api/)
- [API Reference Associated Persons groupQuoteIntents API](https://apis.io/collections/kota/open-kota-groupquoteintents-api/)
- [API Reference Associated Persons groups API](https://apis.io/collections/kota/open-kota-groups-api/)
- [API Reference Associated Persons Health Insurance API](https://apis.io/collections/kota/open-kota-health-insurance-api/)
- [API Reference Associated Persons healthInsurance API](https://apis.io/collections/kota/open-kota-healthinsurance-api/)
- [API Reference Associated Persons Hosted Sessions API](https://apis.io/collections/kota/open-kota-hosted-sessions-api/)
- [API Reference Associated Persons hostedSessions API](https://apis.io/collections/kota/open-kota-hostedsessions-api/)
- [API Reference Associated Persons plans API](https://apis.io/collections/kota/open-kota-plans-api/)
- …and 41 more published on APIs.io

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Kota Api Overlay](https://apis.io/overlays/kota/kota-api-overlay/)
- [Kota Api Reference Overlay](https://apis.io/overlays/kota/kota-api-reference-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Kota Authentication](https://apis.io/security/kota/kota-authentication/)
- [Kota Domain Security](https://apis.io/security/kota/kota-domain-security/)
- [Kota Trust Center](https://apis.io/security/kota/kota-trust-center/)
- [Kota Vulnerability Disclosure](https://apis.io/security/kota/kota-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Kota Plans Pricing](https://apis.io/plans/kota/kota-plans-pricing/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.kota.io/)
- [Documentation](https://docs.kota.io/getting-started)
- [Getting started](https://docs.kota.io/getting-started)
- [API reference](https://docs.kota.io/api-reference)
- [Pricing](https://www.kota.io/pricing)
- [Sign up](https://www.kota.io/demo)
- [Support](https://help.kota.io/en/)
- [Changelog](https://www.kota.io/changelog)
- [Blog](https://www.kota.io/blog)
- [Security](https://www.kota.io/security)
- [Compliance](https://trust.kota.io/)
- [Terms of service](https://www.kota.io/terms-of-service)
- [Privacy policy](https://www.kota.io/privacy-policy)

## API Evangelist rating

**Kin Score 61.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 57.4 |
| Contract governance | 4.5 |
| Operational transparency | 34.2 |
| Developer ergonomics | 74.4 |
| Access clarity | 92.1 |

**Agent readiness 43.2** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 31.6** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/kota/](https://apis.io/providers/kota/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Kota: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/kota/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
