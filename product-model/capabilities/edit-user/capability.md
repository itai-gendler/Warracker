---
domain: admin-actions
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Edit user

An admin changes another account's admin status and active status. The Owner's account is never demoted or deactivated, and admins do not edit their own account here.
