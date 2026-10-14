---
kind: validation
routes:
  web: Web
steps:
- text: The User submits a claim without a claim date
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-claims
- text: The Product reports that the claim date is required
  kind: product
  actor: user
  entities:
  - entity: claim
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

# Add a claim without a claim date

## Trigger

A User submits a claim with no claim date.

## Outcome

The Product refuses: the claim date is required.
