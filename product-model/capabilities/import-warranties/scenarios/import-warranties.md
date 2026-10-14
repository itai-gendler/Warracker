---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Import and picks a CSV file
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The file has the ProductName and PurchaseDate columns and every row is valid
  kind: condition
  entities: []
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product adds a warranty for each row, creating any tag the User does not have yet in grey
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
  - entity: tag
    effect: creates
    facts:
    - Name
    - Color
  contexts:
    web:
      place: web::signed-in::home
- text: The Product reports how many warranties were imported and lists them on Home
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
  target: backend/warranties_routes.py#import_warranties
- kind: code
  role: implementation
  target: frontend/js/components/importExport.js#handleImport
- kind: doc
  role: intent
  target: README.md
---

# Import warranties from CSV

## Trigger

A User moves their warranty records into Warracker from a spreadsheet.

## Outcome

Every row becomes a tracked warranty of the User, and the User sees how many were imported.

## Edge cases

- Header names match regardless of case and surrounding spaces, and a leading byte order mark is ignored.
- Tags and serial numbers may be a JSON list, as Export writes them, or comma-separated.
- A row's Currency is used when it is a supported code; otherwise the User's preferred currency applies.
