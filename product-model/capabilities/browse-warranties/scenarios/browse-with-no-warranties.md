---
kind: edge
routes:
  web: Web
steps:
- text: The User opens Home
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The User has no tracked warranties
  kind: condition
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product shows that there are no warranties yet, offering to add one
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_warranties
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_archived_warranties
- kind: code
  role: implementation
  target: frontend/js/controllers/warrantyListController.js
- kind: code
  role: implementation
  target: frontend/js/lib/warrantyProcessing.js
---

# Browse with no warranties yet

## Trigger

A User with no warranties opens Home.

## Outcome

Home says there are no warranties yet and offers to add one.
