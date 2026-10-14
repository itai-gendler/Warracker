---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses the Archived status
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The Product lists the User's archived warranties, most recently archived first
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Archived at
    - Expiration date
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

# Browse archived warranties

## Trigger

A User wants to see the warranties they archived.

## Outcome

The User sees their archived warranties, most recently archived first, each offering Unarchive and Delete.
