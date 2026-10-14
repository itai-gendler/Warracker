---
appliesTo:
- type: entity
  id: claim
  effect: changes
permits:
- related:
  - verb: has
    entity: warranty
  - verb: owns
    entity: user
- related:
  - verb: has
    entity: warranty
  - verb: owns
    entity: admin
- related:
  - verb: has
    entity: warranty
  - verb: owns
    entity: owner
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#create_claim
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_claim
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_claim
---

# Only the person who added a warranty edits its claims

A claim's details and status are changed only by the person who added its warranty; admins included, nobody else.
