---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Delete on a warranty and confirms
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
- text: The Product deletes the warranty with its documents and their files
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: removes
    from: Tracked
  - entity: document
    effect: removes
    with: warranty
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_warranty
- kind: code
  role: implementation
  target: frontend/js/components/warrantyActions.js
---

# Delete a warranty

## Trigger

A User wants a warranty gone for good.

## Outcome

The warranty, its documents with their files, and its claims are deleted.
