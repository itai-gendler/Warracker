---
appliesTo:
- type: entity
  id: account
  effect: changes
  facts:
  - Application owner
permits:
- actors:
  - owner
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#transfer_ownership
---

# Only the Owner transfers ownership, and only to another active admin

There is one Owner. Only the Owner makes another account the application owner, and only an active account with admin status; the previous Owner remains an admin.
