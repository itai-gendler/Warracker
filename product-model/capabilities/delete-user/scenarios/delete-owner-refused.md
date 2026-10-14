---
kind: validation
routes:
  web: Web
steps:
- text: The Admin chooses Delete for the Owner's account and confirms
  kind: actor
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts:
    - Application owner
  - entity: owner
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::users
- text: The Product reports that the application owner cannot be deleted
  kind: product
  actor: admin
  entities:
  - entity: owner
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::users
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#delete_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Delete the Owner

## Trigger

An Admin tries to delete the Owner's account.

## Outcome

The Product refuses: the application owner cannot be deleted.
