---
entities:
- entity: account
  shows:
  - Username
  - Admin status
  - Active status
  - Application owner
references:
- kind: code
  role: implementation
  target: frontend/settings-new.html
- kind: code
  role: implementation
  target: backend/admin_routes.py#transfer_ownership
---

# Ownership management

Where the Owner chooses another active admin and transfers ownership to them.
