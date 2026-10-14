---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses to sign out
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in
- text: The Product ends the session and opens the sign-in page
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#logout
- kind: code
  role: implementation
  target: frontend/auth.js
---

# Sign out

## Trigger

A signed-in User chooses to sign out.

## Outcome

The User is signed out and on the sign-in page.
