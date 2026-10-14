---
kind: primary
routes:
  web: Web
steps:
- text: The User deletes a tag and confirms
  kind: actor
  actor: user
  entities:
  - entity: tag
    effect: reads
    facts:
    - Name
  contexts:
    web:
      place: web::signed-in::tag-manager
- text: The Product deletes the tag and takes it off every warranty
  kind: product
  actor: user
  entities:
  - entity: tag
    effect: removes
  - entity: warranty
    effect: changes
    facts:
    - Tags
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

# Delete a tag

## Trigger

A User no longer needs a tag.

## Outcome

The tag is gone and no warranty carries it.
