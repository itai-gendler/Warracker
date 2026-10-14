---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Delete on a warranty in the dashboard table and confirms
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
- text: The Product deletes the warranty with its documents and refreshes the dashboard
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
      place: web::signed-in::status-dashboard
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_warranty
- kind: code
  role: implementation
  target: frontend/js/components/warrantyActions.js
---

# Delete a warranty from the status dashboard

## Trigger

A User deletes a warranty from the dashboard table.

## Outcome

The warranty and everything it holds are deleted and the dashboard counts update.
