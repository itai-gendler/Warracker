---
appliesTo:
- type: entity
  id: claim
  effect: removes
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

# Only the person who added a warranty deletes its claims

A claim is deleted only by the person who added its warranty, or together with the warranty itself.
