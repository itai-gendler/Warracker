---
kind: primary
routes:
  web: Web
steps:
- text: The User removes a tag from the warranty and saves
  kind: actor
  actor: user
  entities:
  - entity: tag
    effect: reads
    facts:
    - Name
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-editor
- text: The Product takes the tag off the warranty
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: changes
    facts:
    - Tags
  - entity: tag
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::warranty-editor
references:
- kind: code
  role: implementation
  target: backend/tags_routes.py
- kind: code
  role: implementation
  target: frontend/js/components/tagManager.js
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_warranty
---

# Remove a tag from a warranty

## Trigger

A tag no longer fits a warranty.

## Outcome

The warranty no longer carries the tag.
