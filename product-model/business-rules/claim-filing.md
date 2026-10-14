---
appliesTo:
- type: entity
  id: claim
  effect: creates
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

# Only the person who added a warranty files claims on it

Claims are filed only by the person who added the warranty. Admins cannot file claims on other people's warranties, even though they may edit those warranties.
