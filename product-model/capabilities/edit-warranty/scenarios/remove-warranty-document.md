---
kind: primary
routes:
  web: Web
steps:
- text: The User deletes the manual of the warranty and saves
  kind: actor
  actor: user
  entities:
  - entity: document
    effect: reads
    facts:
    - Kind
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-editor
- text: The Product deletes the document and its file
  kind: product
  actor: user
  entities:
  - entity: document
    effect: removes
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

# Remove a warranty's document

## Trigger

A User no longer wants a manual kept with a warranty.

## Outcome

The warranty no longer holds the document and its file is deleted.
