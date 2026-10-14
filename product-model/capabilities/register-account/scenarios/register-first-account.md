---
kind: primary
routes:
  web: Web
steps:
- text: The Visitor enters a username, email and password
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::registration
- text: No account exists yet
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::public::registration
  actor: visitor
- text: The Product creates the account with full administrative rights, as the installation's owning account, and signs the Visitor in
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

# Register the first account

## Trigger

A Visitor registers on an installation that has no account yet.

## Outcome

The Visitor's account is the installation's Admin and its Owner, whatever the registration setting says.
