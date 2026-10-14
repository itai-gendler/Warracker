---
kind: primary
routes:
  web: Web
steps:
- text: The Admin chooses Edit on a warranty someone else added, in the global scope on Home
  kind: actor
  actor: admin
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
  contexts:
    web:
      place: web::signed-in::home
- text: The Admin changes the warranty's details and saves
  kind: actor
  actor: admin
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
- text: The Product saves the warranty
  kind: product
  actor: admin
  entities:
  - entity: warranty
    effect: changes
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

# Admin edits someone else's warranty

## Trigger

An Admin browsing the global scope corrects a warranty someone else added.

## Outcome

The warranty has the new details; it still belongs to the person who added it.
