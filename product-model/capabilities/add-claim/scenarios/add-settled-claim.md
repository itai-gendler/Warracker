---
kind: primary
routes:
  web: Web
steps:
- text: The User adds a claim with the status Resolved, a resolution and a resolution date
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-claims
- text: The Product adds the resolved claim to the warranty
  kind: product
  actor: user
  entities:
  - entity: claim
    effect: creates
    to: Resolved
    facts:
    - Claim date
    - Claim number
    - Description
    - Resolution
    - Resolution date
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

# Record a claim that is already settled

## Trigger

A User records a past claim that has already been resolved.

## Outcome

The warranty has a Resolved claim with its resolution, and its claim summary is Finished unless another claim is open.
