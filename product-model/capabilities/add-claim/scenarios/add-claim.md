---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses to add a claim and enters its claim date, claim number and description, keeping the status Submitted
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-claims
- text: The Product adds the claim to the warranty
  kind: product
  actor: user
  entities:
  - entity: claim
    effect: creates
    to: Submitted
    facts:
    - Claim date
    - Claim number
    - Description
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

# Add a claim

## Trigger

A User has made a warranty claim with the seller of a product they track.

## Outcome

The warranty has a new Submitted claim and its claim summary is Open.
