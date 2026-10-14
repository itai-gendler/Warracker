---
kind: primary
routes:
  web: Web
steps:
- text: The User opens the status dashboard
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::status-dashboard
- text: The Product counts the User's tracked warranties as active, expiring soon within their expiring soon days, or expired, and their archived ones
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Expiration date
    - Lifetime
    - Expiry status
    - Archived at
  - entity: account
    effect: reads
    facts:
    - Expiring soon days
  contexts:
    web:
      place: web::signed-in::status-dashboard
- text: The Product shows the counts, the total purchase value of tracked warranties, the status distribution, the next 90 days' expiration timeline and the warranties recently expired or expiring soon
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Purchase date
    - Expiration date
    - Expiry status
    - Purchase price
  contexts:
    web:
      place: web::signed-in::status-dashboard
references:
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_statistics
- kind: code
  role: implementation
  target: frontend/status.js
---

# View the status dashboard

## Trigger

A User wants an overview of their coverage.

## Outcome

The User sees the counts, total value, charts and table for their own warranties.

## Edge cases

- The total value adds purchase prices as they are, whatever their currency.
