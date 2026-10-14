---
kind: primary
routes:
  web: Web
steps:
- text: The User enters the product name, purchase date and the exact expiration date
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The expiration date is not before the purchase date
  kind: condition
  entities: []
  contexts:
    web:
      place: web::signed-in::add-warranty
  actor: user
- text: The Product adds the warranty with that expiration date and no warranty period
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

# Add a warranty with an exact expiration date

## Trigger

A User knows the date their warranty ends rather than its length.

## Outcome

The warranty is tracked with the entered expiration date and no warranty period.
