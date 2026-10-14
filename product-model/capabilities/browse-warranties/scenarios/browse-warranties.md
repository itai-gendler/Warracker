---
kind: primary
routes:
  web: Web
steps:
- text: The User opens Home
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The Product restores the default view and saved filters
  kind: product
  actor: user
  entities:
  - entity: account
    effect: reads
    facts:
    - Default view
    - Saved filters
  contexts:
    web:
      place: web::signed-in::home
- text: The Product lists the User's tracked warranties with their expiry status, soonest expiry first
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Purchase date
    - Expiration date
    - Expiry status
    - Lifetime
    - Tags
    - Claim summary
    - Purchase price
    - Serial numbers
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_warranties
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_archived_warranties
- kind: code
  role: implementation
  target: frontend/js/controllers/warrantyListController.js
- kind: code
  role: implementation
  target: frontend/js/lib/warrantyProcessing.js
---

# Browse own warranties

## Trigger

A User opens Home.

## Outcome

The User sees their tracked warranties with each one's expiry status, soonest expiry first and lifetime warranties last, in their default view with their saved filters applied.

## Edge cases

- Prices are shown with the viewer's currency symbol and position.
