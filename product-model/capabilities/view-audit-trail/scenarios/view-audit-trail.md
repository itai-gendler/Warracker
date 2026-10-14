---
kind: primary
routes:
  web: Web
steps:
- text: The Admin chooses View Audit Log
  kind: actor
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::audit-trail
- text: The Product shows the latest 100 audit trail entries, newest first
  kind: product
  actor: admin
  entities:
  - entity: audit-trail-entry
    effect: reads
    facts:
    - Timestamp
    - User
    - Action
    - Details
  contexts:
    web:
      place: web::administration::audit-trail
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_audit_trail
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# View the audit trail

## Trigger

An Admin wants to know who changed accounts or settings.

## Outcome

The Admin sees the latest 100 recorded changes with when, who, what kind and the details.
