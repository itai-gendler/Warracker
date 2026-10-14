---
appliesTo:
- type: entity
  id: warranty
  effect: removes
permits:
- related:
  - verb: owns
    entity: user
- actors:
  - admin
  - owner
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_warranty
- kind: code
  role: implementation
  target: backend/admin_routes.py#delete_user
---

# Only the person who added a warranty, or an admin, deletes it

A warranty is deleted by the person who added it, or by any admin or the Owner, including when their whole account is deleted.
