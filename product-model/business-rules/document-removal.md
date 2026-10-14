---
appliesTo:
- type: entity
  id: document
  effect: removes
permits:
- related:
  - verb: holds
    entity: warranty
  - verb: owns
    entity: user
- actors:
  - admin
  - owner
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_warranty
---

# Only the person who added a warranty, or an admin, removes its documents

Documents are removed from a warranty by whoever may change the warranty: the person who added it, or an admin. Removing a locally stored document deletes its file.
