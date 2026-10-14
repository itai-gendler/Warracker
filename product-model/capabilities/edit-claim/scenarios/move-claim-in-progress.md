---
kind: primary
routes:
  web: Web
steps:
- text: The User edits a Submitted claim, sets its status to In Progress and its claim number, and saves
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts:
    - Claim number
  contexts:
    web:
      place: web::signed-in::warranty-claims
- text: The Product saves the claim
  kind: product
  actor: user
  entities:
  - entity: claim
    effect: changes
    from: Submitted
    to: In Progress
    facts:
    - Claim number
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

# Mark a claim in progress

## Trigger

The seller has started handling a User's claim.

## Outcome

The claim is In Progress and the warranty's claim summary stays Open.
