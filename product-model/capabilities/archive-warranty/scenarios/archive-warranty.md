---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Archive on a warranty and confirms
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
- text: The Product archives the warranty, recording when
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: changes
    from: Tracked
    to: Archived
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

# Archive a warranty

## Trigger

A User no longer needs an expired or unused warranty in view.

## Outcome

The warranty is archived: it moves to the archived list and stops getting reminders.
