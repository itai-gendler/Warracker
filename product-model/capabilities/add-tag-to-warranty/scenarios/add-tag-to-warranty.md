---
kind: primary
routes:
  web: Web
steps:
- text: The User picks one of their tags for the warranty and saves
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
- text: The Product attaches the tag to the warranty
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

# Add a tag to a warranty

## Trigger

A User wants a warranty to show under a tag.

## Outcome

The warranty carries the tag and appears when filtering by it.
