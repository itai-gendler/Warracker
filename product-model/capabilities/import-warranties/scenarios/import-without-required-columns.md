---
kind: validation
routes:
  web: Web
steps:
- text: The User imports a file missing a required column
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The Product reports the missing columns and imports nothing
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

# Import a file without the required columns

## Trigger

A User imports a CSV without a ProductName or PurchaseDate column, or a file that is not a CSV.

## Outcome

Nothing is imported and the User is told which columns are missing or that the file type is wrong.
