---
kind: validation
routes:
  web: Web
steps:
- text: The User enters expiring soon days outside 1 to 365 and saves
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
- text: The Product reports that expiring soon days must be between 1 and 365
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_preferences
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change preferences out of range

## Trigger

A User enters expiring soon days outside 1 to 365.

## Outcome

The Product refuses and the preferences are unchanged.
