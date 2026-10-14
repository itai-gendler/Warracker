---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Unarchive on a warranty in the archived list
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Archived at
  contexts:
    web:
      place: web::signed-in::home
- text: The Product returns the warranty to the main list
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: changes
    from: Archived
    to: Tracked
    facts:
    - Archived at
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#toggle_archive_warranty
- kind: code
  role: implementation
  target: frontend/js/components/warrantyActions.js
---

# Unarchive a warranty

## Trigger

A User needs an archived warranty again.

## Outcome

The warranty is back on the main list, counted on the dashboard and reminded about again.
