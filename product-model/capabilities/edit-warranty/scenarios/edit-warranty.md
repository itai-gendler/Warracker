---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Edit on one of their warranties on Home
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
  contexts:
    web:
      place: web::signed-in::home
- text: The User changes the warranty's details, coverage or links and saves
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Purchase date
    - Warranty period
    - Expiration date
    - Vendor
    - Purchase price
    - Notes
  contexts:
    web:
      place: web::signed-in::warranty-editor
- text: The coverage is valid and its expiration date is not before the purchase date
  kind: condition
  entities: []
  contexts:
    web:
      place: web::signed-in::warranty-editor
  actor: user
- text: The Product saves the warranty with its expiration date worked out again
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: changes
    facts:
    - Product name
    - Purchase date
    - Lifetime
    - Warranty period
    - Expiration date
    - Warranty type
    - Vendor
    - Model number
    - Serial numbers
    - Product URL
    - Purchase price
    - Currency
    - Notes
    - Invoice URL
    - Manual URL
    - Files URL
  contexts:
    web:
      place: web::signed-in::warranty-editor
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_warranty
- kind: code
  role: implementation
  target: frontend/js/components/editModal.js
- kind: code
  role: implementation
  target: frontend/js/components/notes.js
---

# Edit a warranty

## Trigger

A User wants to correct one of their warranties.

## Outcome

The warranty has the new details, with its expiration date worked out again.

## Edge cases

- In the archived list Edit is offered disabled; a warranty is unarchived before it is edited.
