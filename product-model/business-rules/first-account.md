---
appliesTo:
- type: entity
  id: account
  effect: creates
  facts:
  - Admin status
  - Application owner
- type: capability
  id: register-account
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#register
- kind: code
  role: implementation
  target: backend/__init__.py#ensure_owner_exists
---

# The first account becomes the Admin and the Owner

The first account registered on an installation gets admin status and is the application owner; every later registration starts without admin rights. When no Owner exists at start-up, the earliest account is made the Owner.
