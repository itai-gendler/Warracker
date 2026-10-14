---
appliesTo:
- type: entity
  id: tag
  effect: changes
permits:
- related:
  - verb: owns
    entity: user
- related:
  - verb: owns
    entity: admin
- related:
  - verb: owns
    entity: owner
references:
- kind: code
  role: implementation
  target: backend/tags_routes.py#update_tag
- kind: code
  role: implementation
  target: backend/tags_routes.py#delete_tag_endpoint
---

# Only the person who created a tag changes it

Tags are personal: only the person who created a tag renames or recolors it, admins included.
