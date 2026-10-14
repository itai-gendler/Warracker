---
kind: primary
routes:
  web: Web
steps:
- text: The Visitor enters their username or email and password
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
- text: The credentials match an active account
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts:
    - Username
    - Password
    - Active status
  contexts:
    web:
      place: web::public::sign-in
  actor: visitor
- text: The Product signs the Visitor in, records the login time and opens Home
  kind: product
  actor: visitor
  entities:
  - entity: account
    effect: changes
    facts:
    - Last login
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

# Sign in with a password

## Trigger

A Visitor with an active local account wants to use Warracker while OIDC-only login mode is off.

## Outcome

The Visitor is signed in and on Home; the account's last login is now.

## Edge cases

- A signed-in session lasts 24 hours unless the deployment sets another length.
