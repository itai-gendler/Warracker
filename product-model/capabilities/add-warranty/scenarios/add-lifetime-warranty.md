---
kind: primary
routes:
  web: Web
steps:
- text: The User enters the product name and purchase date and marks the warranty as lifetime
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The Product adds the lifetime warranty without an expiration date or period
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
  contexts:
    web:
      place: web::signed-in::add-warranty
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

# Add a lifetime warranty

## Trigger

A User has bought a product with lifetime coverage.

## Outcome

The warranty is tracked as lifetime, with no expiration date, never expiring and never reminded about.
