---
kind: primary
routes:
  web: Web
steps:
- text: The User enters the product name, purchase date and warranty period in years, months and days, with any vendor, model number, serial numbers, type, price, currency, notes and links
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The User attaches an invoice and a product photo, picks tags and reviews the summary
  kind: actor
  actor: user
  entities:
  - entity: tag
    effect: reads
    facts:
    - Name
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The period is not zero and the expiration date it gives is not before the purchase date
  kind: condition
  entities: []
  contexts:
    web:
      place: web::signed-in::add-warranty
  actor: user
- text: The Product adds the warranty with the purchase date plus the period as its expiration date and stores the documents on the server
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
    - Invoice URL
    - Manual URL
    - Files URL
    - Tags
  - entity: document
    effect: creates
    facts:
    - Kind
    - Storage
    - File
    with: warranty
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The Product lists the new warranty on Home
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
  target: backend/warranties_routes.py#add_warranty
- kind: code
  role: implementation
  target: frontend/js/components/addWarrantyForm.js
- kind: code
  role: implementation
  target: backend/utils.py#allowed_file
---

# Add a warranty with a warranty period

## Trigger

A User has bought a product with, say, a two-year warranty.

## Outcome

The warranty is tracked with its expiration date worked out from the purchase date and period, with its invoice and photo stored, and appears on Home.

## Edge cases

- Without a chosen currency the warranty takes the currency of the User's currency symbol, or US dollars.
- Years above 999 and negative or non-numeric parts are refused.
