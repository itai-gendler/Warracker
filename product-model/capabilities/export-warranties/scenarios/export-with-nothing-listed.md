---
kind: edge
routes:
  web: Web
steps:
- text: The User chooses Export
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: No warranty is listed
  kind: condition
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product reports that there are no warranties to export
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: frontend/js/components/importExport.js#exportWarranties
---

# Export with nothing listed

## Trigger

A User chooses Export when no warranty matches the current filters.

## Outcome

No file is downloaded and the User is told there is nothing to export.
