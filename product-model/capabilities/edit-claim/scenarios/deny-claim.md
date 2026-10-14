---
kind: primary
routes:
  web: Web
steps:
- text: The User edits an In Progress claim, sets its status to Denied and enters the resolution
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts:
    - Resolution
  contexts:
    web:
      place: web::signed-in::warranty-claims
- text: The Product saves the claim
  kind: product
  actor: user
  entities:
  - entity: claim
    effect: changes
    from: In Progress
    to: Denied
    facts:
    - Resolution
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

# Deny a claim

## Trigger

The seller refused a User's claim.

## Outcome

The claim is Denied, with the reason as its resolution.
