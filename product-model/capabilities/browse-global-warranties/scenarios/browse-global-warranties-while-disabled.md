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
- text: The global view is disabled
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Global view enabled
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

# Global scope while the global view is disabled

## Trigger

A User looks for the global scope after an Admin disabled the global view.

## Outcome

Only the User's own warranties are available; the global scope is not offered.
