---
kind: validation
routes:
  web: Web
steps:
- text: The User sets the warranty period to zero without an exact date and saves
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-editor
- text: The Product reports that a warranty period or exact expiration date is required
  kind: product
  actor: user
  entities:
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

# Edit a warranty without coverage

## Trigger

A User clears the warranty period of a warranty that is not lifetime and gives no exact date.

## Outcome

The Product refuses: a warranty period or an expiration date is required, and the warranty is unchanged.
