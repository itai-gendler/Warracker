---
kind: validation
routes:
  web: Web
steps:
- text: The Admin saves changes to their own account in the list of people
  kind: actor
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::users
- text: The Product reports that admins cannot modify their own admin status
  kind: product
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::users
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Edit one's own status

## Trigger

An Admin opens Edit User for their own account and saves.

## Outcome

The Product refuses: admins cannot modify their own admin status.
