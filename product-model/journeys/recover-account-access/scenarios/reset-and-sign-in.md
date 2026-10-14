---
kind: primary
result: achieved
routes:
  web: Web
steps:
- text: The Visitor asks for a reset link, follows it and chooses a new password
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::password-reset
  capability: reset-password
- text: The Product sets the new password and opens the sign-in page
  kind: product
  actor: visitor
  entities:
  - entity: account
    effect: changes
    facts:
    - Password
  contexts:
    web:
      place: web::public::password-reset
  capability: reset-password
- text: The Visitor signs in with the new password
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::sign-in
  capability: sign-in
- text: The Product signs the Visitor in and opens Home
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
  capability: sign-in
references:
- kind: code
  role: implementation
  target: frontend/reset-password.html
- kind: code
  role: implementation
  target: frontend/login.html
---

# Reset the password and sign in

## Trigger

A Visitor has forgotten their password.

## Outcome

The Visitor is signed in with the new password.
