---
name: Register a webhook for assessment events
description: Register, list, and manage VISO TRUST outbound webhooks for assessment and relationship lifecycle events.
api: openapi/viso-trust-protecht-openapi-original.json
operations: [registerWebhook, getAllWebhooksForClient, getWebhookByIdForClient, updateWebhook, deleteWebhook]
generated: '2026-07-21'
method: generated
---

# Register a webhook for assessment events

Base URL: `https://app.visotrust.com`. Send `Authorization: Bearer <token>`.

## Steps

1. **Register the webhook** — `POST /api/v1/webhooks` (`registerWebhook`) with a
   `webhookUrl`, a `serviceType` (`GENERIC`, `SLACK`, `DISCORD`, `TEAMS`, or
   `WORKATO`), and an `eventTypes` array selecting from the 15-event catalog in
   `asyncapi/viso-trust-protecht-webhooks.yml` (e.g. `ASSESSMENT_COMPLETED`,
   `RELATIONSHIP_ONBOARDED`, `ARTIFACT_EXPIRING`).
2. **List / inspect** — `GET /api/v1/webhooks` (`getAllWebhooksForClient`) and
   `GET /api/v1/webhooks/{webhookId}` (`getWebhookByIdForClient`).
3. **Update** — `PUT /api/v1/webhooks` (`updateWebhook`) to change the target or
   subscribed event types.
4. **Remove** — `DELETE /api/v1/webhooks/{webhookId}` (`deleteWebhook`).

## Notes
- Subscribing to lifecycle events lets you avoid polling `getAssessment`.
