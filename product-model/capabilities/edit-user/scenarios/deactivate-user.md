---
kind: primary
routes:
  web: Web
steps:
- text: The Admin opens the edit form of another account, turns Active Status off and saves
  kind: actor
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts:
    - Username
    - Active status
  contexts:
    web:
      place: web::administration::users
- text: The Product deactivates the account
  kind: product
  actor: admin
  entities:
  - entity: account
    effect: changes
    facts:
    - Active status
  contexts:
    web:
      place: web::administration::users
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Deactivate a person

## Trigger

An Admin wants to stop someone from signing in without deleting their data.

## Outcome

The account is deactivated: the person cannot sign in and gets no reminders, and everything they keep stays; the change is in the audit trail.

## Edge cases

- Turning Active Status back on lets the person sign in again with everything they kept.
