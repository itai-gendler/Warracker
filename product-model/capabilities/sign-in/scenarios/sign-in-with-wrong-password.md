---
kind: validation
routes:
  web: Web
steps:
- text: The Visitor enters a username or email and a password
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
- text: No account matches the credentials
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::public::sign-in
  actor: visitor
- text: The Product reports an invalid username or password
  kind: product
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#login
- kind: code
  role: implementation
  target: backend/oidc_handler.py#oidc_callback_route
- kind: code
  role: implementation
  target: frontend/login.html
---

# Sign in with a wrong password

## Trigger

A Visitor enters a username or password that does not match.

## Outcome

The Product reports an invalid username or password and the Visitor stays signed out.
