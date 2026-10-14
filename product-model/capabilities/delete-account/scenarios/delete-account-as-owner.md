---
kind: validation
routes:
  web: Web
steps:
- text: The Owner confirms deleting their account
  kind: actor
  actor: owner
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::settings
- text: The Product reports that the application owner cannot delete their account before transferring ownership
  kind: product
  actor: owner
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#delete_account
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Owner tries to delete their account

## Trigger

The Owner tries to delete their own account.

## Outcome

The Product refuses and asks for ownership to be transferred first; nothing is deleted.
