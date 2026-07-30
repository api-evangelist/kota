# Kota

Kota is a Dublin-headquartered employee benefits platform that gives payroll, HR and
employer-of-record platforms embedded access to health insurance, workplace pensions, life
assurance, flexible benefits and spend cards across Ireland, the UK, Spain and other markets.

Kota Embedded is sold as three developer products — **Hosted** (redirect to a Kota-run experience),
**Embed** (the Kota.js SDK mounts themed employer and employee benefit UIs into your product), and
**API** (build a fully custom benefits journey). The Kota API is a published OpenAPI 3.1 contract at
`https://api.kota.io/openapi.json` covering employers, employees, groups, group policies, policies,
plans, health insurance quotes and offers, contribution reports, associated persons/dependents, and
the family of intent resources that model each step of the benefits lifecycle.

- Website — https://www.kota.io/
- Developer docs — https://docs.kota.io/getting-started
- API reference — https://docs.kota.io/api-reference
- Trust Centre — https://trust.kota.io/

Backed by: eqt-ventures, northzone

## What's captured here

| Area | Artifact |
|---|---|
| OpenAPI (85 operations, 61 webhooks) | `openapi/` |
| Webhook / event catalog | `asyncapi/kota-webhooks.yml` |
| Authentication profile | `authentication/` |
| API conventions (idempotency, pagination, tracing) | `conventions/` |
| RFC 9457 error catalog | `errors/` |
| Lifecycle & versioning | `lifecycle/` |
| Conformance & compliance posture | `conformance/` |
| Data model / ERD | `data-model/` |
| Agent Skills (6 flows) | `skills/` |
| MCP server (hosted docs MCP) | `mcp/` |
| llms.txt (published by Kota) | `llms/` |
| Packages / SDK | `packages/` |
| Embedded UI components | `components/` |
| Sandbox / test environment | `sandbox/` |
| Product changelog | `changelog/` |
| Security, trust centre, disclosure | `security/` |
| Well-known discovery probe | `well-known/` |
| Agentic access contracts (172 ops) | `agentic-access/` |
| OpenAPI overlays | `overlays/` |
