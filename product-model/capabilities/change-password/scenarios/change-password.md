---
kind: primary
routes:
  web: Web
steps:
- text: The User enters their current password and a new password twice
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
- text: The current password matches and the new one meets the strength rule
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts:
    - Password
  contexts:
    web:
      place: web::signed-in::settings
  actor: user
- text: The Product sets the new password
  kind: product
  actor: user
  entities:
  - entity: account
    effect: changes
    facts:
    - Password
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#change_password
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change password

## Trigger

A User with a local account wants a new password.

## Outcome

The account has the new password.
