---
kind: primary
routes:
  web: Web
steps:
- text: The User enters a tag name and picks a color in the tag manager
  kind: actor
  actor: user
  entities:
  - entity: tag
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::tag-manager
- text: The name has at most 50 characters and none of the User's tags has it
  kind: condition
  entities:
  - entity: tag
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::tag-manager
  actor: user
- text: The Product creates the tag
  kind: product
  actor: user
  entities:
  - entity: tag
    effect: creates
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

# Create a tag

## Trigger

A User wants to group warranties, for example by room.

## Outcome

The User has a new tag to attach to warranties and filter by.
