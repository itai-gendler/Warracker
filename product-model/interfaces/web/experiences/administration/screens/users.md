---
entities:
- entity: account
  shows:
  - Username
  - Email
  - First name
  - Last name
  - Admin status
  - Application owner
  - Active status
  - Last login
  collects:
  - Admin status
  - Active status
references:
- kind: code
  role: implementation
  target: frontend/settings-new.js
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_all_users
---

# Users

Every account on the installation, the Owner marked, with the forms for editing an account's admin and active status and for deleting it.
