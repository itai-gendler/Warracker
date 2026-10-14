---
kind: edge
routes:
  web: Web
steps:
- text: The User imports a file mixing valid and invalid rows
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: Some rows are valid and others are not
  kind: condition
  entities: []
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product adds a warranty for each valid row and reports the number imported and the number failed, with each failed row's reasons
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: creates
    to: Tracked
    facts:
    - Product name
    - Purchase date
    - Lifetime
    - Warranty period
    - Expiration date
    - Warranty type
    - Vendor
    - Model number
    - Serial numbers
    - Product URL
    - Purchase price
    - Currency
    - Notes
    - Tags
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

# Import a file with some invalid rows

## Trigger

A User imports a file where some rows lack a product name, have a bad date, no coverage or a negative price.

## Outcome

The valid rows are imported and the User is told how many rows failed.
