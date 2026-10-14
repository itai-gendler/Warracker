---
appliesTo:
- type: entity
  id: account
  effect: changes
  facts:
  - Last login
permits:
- actors:
  - visitor
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#login
- kind: code
  role: implementation
  target: backend/oidc_handler.py#oidc_callback_route
---

# Signing in records the last login

Every successful sign-in, with a password or single sign-on, records the time on the account; nothing else changes it.
