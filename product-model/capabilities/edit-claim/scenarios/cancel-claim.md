---
kind: primary
routes:
  web: Web
steps:
- text: The User edits a Submitted claim and sets its status to Cancelled
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
    from: Submitted
    to: Cancelled
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

# Cancel a claim

## Trigger

A User withdraws a claim they filed.

## Outcome

The claim is Cancelled.

## Edge cases

- Any status can be set from any other; a Cancelled or Resolved claim can be reopened by setting it back to Submitted or In Progress.
