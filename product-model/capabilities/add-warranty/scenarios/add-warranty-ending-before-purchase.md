---
kind: validation
routes:
  web: Web
steps:
- text: The User enters an expiration date before the purchase date and submits
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The Product reports that the expiration date cannot be before the purchase date
  kind: product
  actor: user
  entities: []
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

# Add a warranty that ends before its purchase

## Trigger

A User enters an exact expiration date earlier than the purchase date.

## Outcome

The Product refuses: the expiration date cannot be before the purchase date, and nothing is added.
