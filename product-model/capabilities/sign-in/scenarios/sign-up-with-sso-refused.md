---
kind: validation
routes:
  web: Web
steps:
- text: The Visitor authenticates at the OIDC provider
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
- text: No account holds the provider identity and registration is disabled, the provider sends no email, or a local account uses that email
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Registration enabled
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::public::sign-in
  actor: visitor
- text: The Product returns the Visitor to the sign-in page explaining why no account was created
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

# Single sign-on refused for a new person

## Trigger

A Visitor without an account signs in through the provider while registration is disabled, or the provider sends no email, or a local account already uses that email.

## Outcome

The Visitor is back on the sign-in page with the reason, and no account is created.
