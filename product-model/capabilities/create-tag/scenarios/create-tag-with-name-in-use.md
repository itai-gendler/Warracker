---
kind: validation
routes:
  web: Web
steps:
- text: The User enters the name of one of their existing tags
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
- text: The Product reports that a tag with this name already exists for the account
  kind: product
  actor: user
  entities:
  - entity: account
    effect: reads
    facts: []
  - entity: tag
    effect: reads
    facts: []
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

# Create a tag with a name in use

## Trigger

A User enters the name of a tag they already have.

## Outcome

The Product refuses: a tag with this name already exists for the account.
