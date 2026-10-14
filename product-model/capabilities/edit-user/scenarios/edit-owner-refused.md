---
kind: validation
routes:
  web: Web
steps:
- text: The Admin turns off Admin Status or Active Status for the Owner's account and saves
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
- text: The Product reports that the application owner cannot be demoted or deactivated
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
  target: backend/admin_routes.py#update_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Demote or deactivate the Owner

## Trigger

An Admin tries to remove the Owner's admin status or deactivate the Owner.

## Outcome

The Product refuses and the Owner's account is unchanged.
