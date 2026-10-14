---
kind: validation
routes:
  web: Web
steps:
- text: The User imports a file in which every row is invalid
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The Product imports nothing and reports that the import failed
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#import_warranties
- kind: code
  role: implementation
  target: frontend/js/components/importExport.js#handleImport
- kind: doc
  role: intent
  target: README.md
---

# Import a file with no valid rows

## Trigger

A User imports a file in which every row is invalid.

## Outcome

Nothing is imported and the User is told the import failed.
