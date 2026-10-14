---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses the global scope on Home
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The global view is enabled and not restricted to administrators
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Global view enabled
    - Global view admin only
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product lists every tracked warranty with the name of the person who added it, other people's without edit, archive or delete
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Expiration date
    - Expiry status
    - Tags
    - Claim summary
  - entity: account
    effect: reads
    facts:
    - First name
    - Last name
    - Username
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

# Browse everyone's warranties

## Trigger

A User wants to see the warranties everyone on the installation keeps.

## Outcome

Home lists everyone's tracked warranties grouped by who added them, other people's offering only to view their claims.

## Edge cases

- The archived list in the global scope shows everyone's archived warranties the same way.
