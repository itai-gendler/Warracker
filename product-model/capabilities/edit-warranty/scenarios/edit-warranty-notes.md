---
kind: primary
routes:
  web: Web
steps:
- text: The User opens a warranty's notes on Home, edits them and saves
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Notes
  contexts:
    web:
      place: web::signed-in::home
- text: The Product saves the notes to the warranty
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: changes
    facts:
    - Notes
  contexts:
    web:
      place: web::signed-in::home
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

# Edit a warranty's notes

## Trigger

A User opens a warranty's notes from Home to add something.

## Outcome

The warranty has the new notes.
