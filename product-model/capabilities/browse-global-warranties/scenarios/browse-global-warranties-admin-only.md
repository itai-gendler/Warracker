---
kind: validation
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
- text: The global view is restricted to administrators
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Global view admin only
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product offers only the personal scope
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_global_warranties
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_global_warranties_archived
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_global_statistics
- kind: code
  role: implementation
  target: frontend/js/components/warrantyRenderer.js
---

# Global scope limited to admins

## Trigger

A User without admin rights looks for the global scope while it is limited to admins.

## Outcome

The global scope is not offered to the User, while Admins still have it.
