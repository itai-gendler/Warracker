---
appliesTo:
- type: entity
  id: account
  effect: removes
- type: entity
  id: tag
- type: entity
  id: warranty
  effect: removes
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#delete_account
- kind: code
  role: implementation
  target: backend/admin_routes.py#delete_user
---

# Deleting an account deletes its warranties and tags

When an account is deleted, by its holder or by an admin, every warranty it added, tracked or archived, with everything those warranties hold, and every tag it created are deleted with it.
