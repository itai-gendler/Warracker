---
kind: validation
routes:
  web: Web
steps:
- text: The User enters an email address another account uses and saves
  kind: actor
  actor: user
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::settings
- text: The Product reports that the email address is already in use
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_profile
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Edit profile with an email in use

## Trigger

A User enters an email another account already has.

## Outcome

The Product reports that the email is already in use and the account is unchanged.
