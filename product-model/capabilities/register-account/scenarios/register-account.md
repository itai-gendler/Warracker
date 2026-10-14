---
kind: primary
routes:
  web: Web
steps:
- text: The Visitor enters a username, email, password and, optionally, a first and last name
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::registration
- text: Registration is enabled and the username and email are not in use
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Registration enabled
  contexts:
    web:
      place: web::public::registration
  actor: visitor
- text: The Product creates the active local account as an ordinary account and signs the Visitor in
  kind: product
  actor: visitor
  entities:
  - entity: account
    effect: creates
    facts:
    - Username
    - Email
    - Password
    - First name
    - Last name
    - Sign-in method
    - Admin status
    - Application owner
    - Active status
    - Last login
  contexts:
    web:
      place: web::public::registration
- text: The Product opens Home
  kind: product
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::registration
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#register
- kind: code
  role: implementation
  target: frontend/register.html
---

# Register an account

## Trigger

A Visitor wants an account on an installation that has accounts and allows registration.

## Outcome

The Visitor has a local account without admin rights and is signed in to Home.

## Edge cases

- A password shorter than 8 characters, without an upper-case letter, a lower-case letter and a digit, or longer than 72 bytes is refused before anything is created.
- An email address that is not well formed is refused.
