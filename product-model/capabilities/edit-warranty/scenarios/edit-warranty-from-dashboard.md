---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Edit on a warranty in the dashboard table
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
  contexts:
    web:
      place: web::signed-in::status-dashboard
- text: The User changes the warranty's details and saves
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
- text: The Product saves the warranty and refreshes the dashboard
  kind: product
  actor: user
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

# Edit a warranty from the status dashboard

## Trigger

A User spots a mistake in the status dashboard's table.

## Outcome

The warranty has the new details and the dashboard reflects them.
