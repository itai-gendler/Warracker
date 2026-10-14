---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#change_password
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change password

A person with a local account changes their password by giving the current one.
