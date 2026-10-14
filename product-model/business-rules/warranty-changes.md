---
appliesTo:
- type: entity
  id: warranty
  effect: changes
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
  target: backend/warranties_routes.py#update_warranty
- kind: code
  role: implementation
  target: backend/warranties_routes.py#toggle_archive_warranty
---

# Only the person who added a warranty, or an admin, changes it

A warranty is edited, archived, unarchived, tagged and untagged by the person who added it, or by any admin or the Owner. Everyone else sees it read-only through the global view.
