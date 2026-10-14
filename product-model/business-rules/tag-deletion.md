---
appliesTo:
- type: entity
  id: tag
  effect: removes
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

# Only the person who created a tag deletes it

Only the person who created a tag deletes it, or it goes with their account.
