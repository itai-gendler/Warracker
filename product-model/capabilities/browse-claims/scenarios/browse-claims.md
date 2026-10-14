---
kind: primary
routes:
  web: Web
steps:
- text: The User asks to see what has been filed against one of their warranties
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Claim summary
  contexts:
    web:
      place: web::signed-in::home
- text: The Product lists the warranty's claims with their status, newest claim date first
  kind: product
  actor: user
  entities:
  - entity: claim
    effect: reads
    facts:
    - Claim date
    - Claim number
    - Description
    - Resolution
    - Resolution date
  - entity: warranty
    effect: reads
    facts:
    - Product name
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

# Browse a warranty's claims

## Trigger

A User checks how the claims on one of their warranties are going.

## Outcome

The User sees the warranty's claims, newest claim date first, and can add, edit and delete them.
