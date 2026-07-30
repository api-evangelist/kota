---
name: Consume Kota events and webhooks
description: Handle Kota's asynchronous event surface — receive webhooks, reconcile with the
  pollable events resource, replay missed deliveries, and act on time-sensitive required actions.
api: openapi/kota-openapi-original.json
base_url: https://api.kota.io
test_base_url: https://test.api.kota.io
operations:
  - ListEvents
  - RetrieveEvent
  - ReplayEvent
  - ListWebhookEndpoints
  - RetrieveWebhookEndpoint
---

# Consume Kota events and webhooks

Benefits work is asynchronous: insurers respond on their own timeline, quotes need employer action,
policies activate later. Kota publishes every state change as an Event, delivered by webhook and
also readable from the API.

## Steps

1. **Confirm your endpoints.** Call `ListWebhookEndpoints` and `RetrieveWebhookEndpoint` to see
   what is registered. Endpoint creation is currently handled by your Kota contact rather than
   self-serve; the docs note management endpoints are coming.
2. **Receive and acknowledge fast.** Return 2xx quickly, queue the work, and process out of band.
   Some actions emit multiple events.
3. **Read state from the event body.** An event's `data` field embeds the resource's state at the
   time of the change. Re-fetch the resource when you need current state instead.
4. **Handle the two critical events immediately.**
   - `employer.health_insurance.quote.action_required`
   - `employee.health_insurance.offer.action_required`

   Both carry a `required_action` object. Map `reason` to your message title,
   `reason_description` to the body, and display `due_at` prominently. Use Kota's wording — writing
   your own language around insurance sales and renewals risks stepping into regulated activity;
   make clear the language comes from Kota.
5. **Reconcile with polling.** Call `ListEvents` on a schedule to catch anything a failed delivery
   missed, and `RetrieveEvent` for a specific one. Retrieval is guaranteed for **30 days** only —
   persist anything you need beyond that window.
6. **Replay what you dropped.** Call `ReplayEvent` to have Kota re-deliver an event to your
   endpoints. Send `Idempotency-Key: <uuid-v4>`.

## Event families

- **v1** — the legacy family (employer, employee, health insurance quote/offer/policy,
  contribution report).
- **v2** — the current family; same events plus groups (`group.created`, `group.ready`,
  `group.employee.added`, `group.employee.eligible`, `group.employee.moved`), policies
  (`policy.scheduled`, `policy.active`, `policy.imported`, `policy.expired`, `policy.cancelled`,
  `policy.updated`), renewals (`policy.renewal.opened`, `policy.renewal.renewed`) and the group
  policy equivalents.

Build new integrations on v2. The full catalog is in `asyncapi/kota-webhooks.yml`.

## Rules

- Make handlers idempotent — assume at-least-once delivery and design for duplicate events.
- Do not infer ordering from arrival order; verify against the resource where sequence matters.
- Kota publishes no AsyncAPI document. The event surface is defined as OpenAPI 3.1 `webhooks` in
  the published spec.
