---
kind: primary
routes:
  web: Web
steps:
- text: The User changes their first name, last name or email and saves
  kind: actor
  actor: user
  entities:
  - entity: account
    effect: reads
    facts:
    - First name
    - Last name
    - Email
  contexts:
    web:
      place: web::signed-in::settings
- text: Both names are given and the email is well formed and not used by another account
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::settings
  actor: user
- text: The Product saves the name and email to the account
  kind: product
  actor: user
  entities:
  - entity: account
    effect: changes
    facts:
    - First name
    - Last name
    - Email
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

# Edit profile

## Trigger

A User with a local account wants to correct their name or email.

## Outcome

The account has the new name and email.
