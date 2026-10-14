---
kind: validation
routes:
  web: Web
steps:
- text: The Owner confirms a transfer to an account without admin status or a deactivated one
  kind: actor
  actor: owner
  entities:
  - entity: account
    effect: reads
    facts:
    - Admin status
    - Active status
  - entity: admin
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::ownership-management
- text: The Product reports that ownership can only be transferred to another active admin
  kind: product
  actor: owner
  entities:
  - entity: admin
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::ownership-management
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#transfer_ownership
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Transfer ownership to someone who is not an active admin

## Trigger

The Owner tries to transfer ownership to an account without admin status or a deactivated one.

## Outcome

The Product refuses: ownership goes only to another active admin.

## Edge cases

- Only active admins other than the Owner are offered.
