---
kind: primary
routes:
  web: Web
steps:
- text: The User changes a tag's name or color and saves
  kind: actor
  actor: user
  entities:
  - entity: tag
    effect: reads
    facts:
    - Name
    - Color
  contexts:
    web:
      place: web::signed-in::tag-manager
- text: The new name is not used by another of the User's tags
  kind: condition
  entities:
  - entity: tag
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::tag-manager
  actor: user
- text: The Product saves the tag
  kind: product
  actor: user
  entities:
  - entity: tag
    effect: changes
    facts:
    - Name
    - Color
  contexts:
    web:
      place: web::signed-in::tag-manager
references:
- kind: code
  role: implementation
  target: backend/tags_routes.py
- kind: code
  role: implementation
  target: frontend/js/components/tagManager.js
---

# Edit a tag

## Trigger

A User wants a clearer tag name or color.

## Outcome

The tag has the new name and color everywhere it appears.
