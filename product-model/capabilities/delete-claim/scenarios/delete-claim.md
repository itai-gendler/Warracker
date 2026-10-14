---
kind: primary
routes:
  web: Web
steps:
- text: The User deletes a claim and confirms
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts:
    - Claim date
  contexts:
    web:
      place: web::signed-in::warranty-claims
- text: The Product deletes the claim
  kind: product
  actor: user
  entities:
  - entity: claim
    effect: removes
    from: Submitted
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

# Delete a claim

## Trigger

A User recorded a claim by mistake.

## Outcome

The claim is gone and the warranty's claim summary is worked out again.
