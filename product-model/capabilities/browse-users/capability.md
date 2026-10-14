---
domain: admin-actions
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_all_users
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Browse users

An admin lists every account on the installation, newest first, with its name, email, status, role and last login, the Owner marked.
