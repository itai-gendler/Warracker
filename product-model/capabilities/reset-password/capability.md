---
availability:
- place: web::public
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#request_password_reset
- kind: code
  role: implementation
  target: backend/auth_routes.py#reset_password
- kind: code
  role: implementation
  target: frontend/reset-password.html
---

# Reset password

A person who forgot their password asks for a reset link by email and, following it within 24 hours, chooses a new password, then signs in again.
