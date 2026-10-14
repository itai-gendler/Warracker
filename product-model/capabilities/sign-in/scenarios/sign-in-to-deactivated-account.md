---
kind: validation
routes:
  web: Web
steps:
- text: The Visitor enters correct credentials
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
- text: The account is deactivated
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts:
    - Active status
  contexts:
    web:
      place: web::public::sign-in
  actor: visitor
- text: The Product reports that the account is inactive
  kind: product
  actor: visitor
  entities:
  - entity: account
    effect: reads
    facts: []
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

# Sign in to a deactivated account

## Trigger

A Visitor signs in with the correct password of an account an Admin deactivated.

## Outcome

The Product reports that the account is inactive and the Visitor stays signed out.
