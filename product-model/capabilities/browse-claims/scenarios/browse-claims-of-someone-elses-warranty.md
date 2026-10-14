---
kind: primary
routes:
  web: Web
steps:
- text: The User asks to see what has been filed against a warranty someone else added, in the global scope
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
- text: The global view is enabled and not restricted to administrators
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Global view enabled
    - Global view admin only
  contexts:
    web:
      place: web::signed-in::warranty-claims
  actor: user
- text: The Product lists the claims read-only
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

# Browse the claims of someone else's warranty

## Trigger

A User in the global scope opens the claims of a warranty someone else added.

## Outcome

The User sees the claims read-only, with no way to add, edit or delete them.
