---
kind: primary
routes:
  web: Web
steps:
- text: The Visitor chooses to sign in with the provider
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
- text: The Product sends the Visitor to the OIDC provider
  kind: product
  actor: visitor
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - OIDC SSO enabled
    - Client ID
    - Issuer URL
    - Scope
  contexts:
    web:
      place: web::public::sign-in
- text: The Visitor authenticates at the OIDC provider
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
- text: The provider identity matches an active OIDC SSO account
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts:
    - Sign-in method
    - Active status
  contexts:
    web:
      place: web::public::sign-in
  actor: visitor
- text: The Product updates the account with the name and email the provider sends and signs the Visitor in
  kind: product
  actor: visitor
  entities:
  - entity: account
    effect: changes
    facts:
    - First name
    - Last name
    - Email
    - Last login
  contexts:
    web:
      place: web::public::sign-in
- text: The Product opens Home
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

# Sign in with single sign-on

## Trigger

A Visitor whose OIDC SSO account already exists chooses single sign-on while OIDC SSO is enabled.

## Outcome

The Visitor is signed in and on Home, with the name and email the provider holds.

## Decision points

### Admin group

Is an OIDC admin group configured?

- Configured → the Product gives the account admin status exactly when the provider lists the Visitor in that group, then signs the Visitor in.
- Not configured → the account keeps its admin status, then the Visitor is signed in.

## Edge cases

- A failed exchange with the provider returns the Visitor to the sign-in page with the reason.
