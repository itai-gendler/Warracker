---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#delete_account
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Delete account

A person permanently deletes their own account with all their warranties and tags. The Owner cannot delete their account.
