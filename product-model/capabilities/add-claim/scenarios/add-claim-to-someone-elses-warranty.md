---
kind: validation
routes:
  web: Web
steps:
- text: The Admin submits a claim on a warranty someone else added
  kind: actor
  actor: admin
  entities:
  - entity: warranty
    effect: reads
    facts: []
  - entity: claim
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-claims
- text: The Product reports that the warranty was not found or access is denied
  kind: product
  actor: admin
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-claims
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_claims
- kind: code
  role: implementation
  target: backend/warranties_routes.py#create_claim
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_claim
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_claim
- kind: code
  role: implementation
  target: frontend/js/components/claims.js
---

# Admin adds a claim to someone else's warranty

## Trigger

An Admin in the global scope tries to add a claim to a warranty someone else added.

## Outcome

The Product refuses: claims are kept only by the person who added the warranty, admins included.
