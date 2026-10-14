---
kind: validation
routes:
  web: Web
steps:
- text: The Visitor follows an old link and chooses a new password
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::password-reset
- text: The link has expired or was already used
  kind: condition
  entities: []
  contexts:
    web:
      place: web::public::password-reset
  actor: visitor
- text: The Product reports that the link is invalid or expired
  kind: product
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::password-reset
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#request_password_reset
- kind: code
  role: implementation
  target: backend/auth_routes.py#reset_password
- kind: code
  role: implementation
  target: frontend/reset-password.html
---

# Reset with an expired or used link

## Trigger

A Visitor follows a reset link that is older than 24 hours or was already used.

## Outcome

The Product reports an invalid or expired link and the password is unchanged.
