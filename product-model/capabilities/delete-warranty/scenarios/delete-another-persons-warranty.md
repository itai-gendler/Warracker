---
kind: primary
routes:
  web: Web
steps:
- text: The Admin chooses Delete on a warranty someone else added, in the global scope, and confirms
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
- text: The Product deletes the warranty with its documents
  kind: product
  actor: admin
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

# Admin deletes someone else's warranty

## Trigger

An Admin removes a warranty someone else added, from the global scope.

## Outcome

That person's warranty and everything it holds are deleted.
