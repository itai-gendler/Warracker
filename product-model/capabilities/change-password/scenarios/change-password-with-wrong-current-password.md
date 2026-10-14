---
kind: validation
routes:
  web: Web
steps:
- text: The User enters a wrong current password and a new password
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
- text: The Product reports that the current password is incorrect
  kind: product
  actor: user
  entities: []
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

# Change password with a wrong current password

## Trigger

A User enters a current password that does not match.

## Outcome

The Product reports an incorrect current password and the password is unchanged.
