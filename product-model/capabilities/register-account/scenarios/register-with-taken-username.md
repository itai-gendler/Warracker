---
kind: validation
routes:
  web: Web
steps:
- text: The Visitor submits a username or email that is already in use
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::registration
- text: The Product reports that the username or email already exists
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

# Register with a username or email already in use

## Trigger

A Visitor registers with a username or email another account already has.

## Outcome

The Product refuses: the username or email already exists, and no account is created.
