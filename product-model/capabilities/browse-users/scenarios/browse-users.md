---
kind: primary
routes:
  web: Web
steps:
- text: The Admin opens the list of people on the installation
  kind: actor
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product lists every account, newest first
  kind: product
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts:
    - Username
    - Email
    - First name
    - Last name
    - Admin status
    - Application owner
    - Active status
    - Last login
  contexts:
    web:
      place: web::administration::users
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_all_users
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Browse users

## Trigger

An Admin chooses Show Users List in the admin actions.

## Outcome

The Admin sees every account with its email, active and admin status, the Owner marked with a crown, and when each last logged in.
