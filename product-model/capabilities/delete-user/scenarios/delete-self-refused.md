---
kind: validation
routes:
  web: Web
steps:
- text: The Admin chooses Delete for their own account and confirms
  kind: actor
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::users
- text: The Product reports that admins cannot delete their own account here
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
  target: backend/admin_routes.py#delete_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Delete oneself from the users list

## Trigger

An Admin chooses Delete for their own account in the users list.

## Outcome

The Product refuses; an admin deletes their own account from their settings instead.
