---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Delete on a warranty in the archived list and confirms
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
- text: The Product deletes the warranty with its documents
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: removes
    from: Archived
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

# Delete an archived warranty

## Trigger

A User clears out an archived warranty.

## Outcome

The archived warranty and everything it holds are deleted.
