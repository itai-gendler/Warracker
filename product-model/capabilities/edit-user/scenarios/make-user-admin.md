---
kind: primary
routes:
  web: Web
steps:
- text: The Admin opens the edit form of another account, turns Admin Status on and saves
  kind: actor
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts:
    - Username
    - Admin status
  contexts:
    web:
      place: web::administration::users
- text: The Product gives the account admin status
  kind: product
  actor: admin
  entities:
  - entity: account
    effect: changes
    facts:
    - Admin status
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

# Give a person admin status

## Trigger

An Admin wants another person to help administer the installation.

## Outcome

The person's account has admin status and the change is in the audit trail.
