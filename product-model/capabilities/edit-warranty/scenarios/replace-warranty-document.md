---
kind: primary
routes:
  web: Web
steps:
- text: The User uploads a new invoice for the warranty and saves
  kind: actor
  actor: user
  entities:
  - entity: document
    as: old-document
    effect: reads
    facts:
    - Kind
    - Storage
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-editor
- text: The Product deletes the old document and stores the new one with the warranty
  kind: product
  actor: user
  entities:
  - entity: document
    as: old-document
    effect: removes
  - entity: document
    as: new-document
    effect: creates
    facts:
    - Kind
    - Storage
    - File
  - entity: warranty
    effect: reads
    facts: []
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

# Replace a warranty's document

## Trigger

A User has a better scan of a receipt already kept with a warranty.

## Outcome

The warranty holds the new file in place of the old one, which is deleted.
