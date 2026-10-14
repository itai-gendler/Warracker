---
kind: primary
routes:
  web: Web
steps:
- text: The User edits an In Progress claim and sets its status to Approved
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts: []
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
    to: Approved
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

# Approve a claim

## Trigger

The seller accepted a User's claim.

## Outcome

The claim is Approved.
