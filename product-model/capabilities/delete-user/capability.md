---
domain: admin-actions
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#delete_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Delete user

An admin permanently deletes another person's account with all their warranties and tags. The Owner's account is never deleted, and admins do not delete themselves here.
