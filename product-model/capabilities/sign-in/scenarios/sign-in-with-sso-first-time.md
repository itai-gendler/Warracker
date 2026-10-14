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
- text: The Visitor authenticates at the OIDC provider
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
- text: No account holds the provider identity, registration is enabled and the provider sends an email no local account uses
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
- text: The Product creates an active OIDC SSO account from the provider's username, name and email and signs the Visitor in
  kind: product
  actor: visitor
  entities:
  - entity: account
    effect: creates
    facts:
    - Username
    - Email
    - First name
    - Last name
    - Sign-in method
    - Admin status
    - Active status
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

# Sign in with single sign-on for the first time

## Trigger

A Visitor without an account signs in through the OIDC provider while registration is enabled.

## Outcome

The Visitor has a new OIDC SSO account and is signed in on Home.

## Decision points

### Admin status of the new account

Is an OIDC admin group configured?

- Configured → the account has admin status when the provider lists the Visitor in that group.
- Not configured → the account has admin status only when it is the first account.

## Edge cases

- A username already taken gets a short random suffix.
