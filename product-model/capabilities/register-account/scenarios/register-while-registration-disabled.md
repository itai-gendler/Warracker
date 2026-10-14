---
kind: validation
routes:
  web: Web
steps:
- text: The Visitor submits the registration form
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::registration
- text: Registration is disabled and accounts already exist
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
      place: web::public::registration
  actor: visitor
- text: The Product reports that registration is currently disabled
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

# Register while registration is disabled

## Trigger

A Visitor tries to register after an Admin has turned registration off.

## Outcome

The Product refuses: registration is currently disabled, and no account is created.

## Edge cases

- The registration page reads the setting and shows that registration is disabled before anything is submitted.
