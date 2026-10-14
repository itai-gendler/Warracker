---
appliesTo:
- type: capability
  id: reset-password
- type: entity
  id: account
  facts:
  - Password
  - Email
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#request_password_reset
- kind: code
  role: implementation
  target: backend/auth_routes.py#reset_password
---

# A password reset link works once, within 24 hours

A reset link expires 24 hours after it was requested, stops working once used, and is replaced by any newer request. Asking for a link never reveals whether an email is registered.
