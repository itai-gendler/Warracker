---
kind: edge
routes:
  web: Web
steps:
- text: The User imports a file with a row repeating a product name and purchase date
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The User already has a warranty with that product name and purchase date
  kind: condition
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Purchase date
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product adds the warranty with the first free numbered suffix on its product name
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

# Import a warranty that is already there

## Trigger

A User imports a row whose product name and purchase date match a warranty they already have, or an earlier row of the same file.

## Outcome

The row is imported under a numbered name, such as "Dishwasher (1)", instead of being refused.
