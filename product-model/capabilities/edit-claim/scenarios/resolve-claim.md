---
kind: primary
routes:
  web: Web
steps:
- text: The User edits an In Progress claim, sets its status to Resolved and enters the resolution and resolution date
  kind: actor
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts:
    - Resolution
    - Resolution date
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
    to: Resolved
    facts:
    - Resolution
    - Resolution date
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

# Resolve a claim

## Trigger

A User's claim has been settled.

## Outcome

The claim is Resolved with its resolution; with no other open claim, the warranty's claim summary is Finished.
