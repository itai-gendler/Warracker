---
kind: edge
routes:
  web: Web
steps:
- text: The Visitor enters an email address
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::password-reset
- text: No account has that email
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::public::password-reset
  actor: visitor
- text: The Product says a link is on its way if the email is registered, sending nothing
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

# Ask for a reset with an unknown email

## Trigger

A Visitor asks for a reset link for an email no account has.

## Outcome

The Visitor sees the same message as for a registered email and no email is sent.

## Edge cases

- When the email cannot be sent, the Visitor sees the same message.
