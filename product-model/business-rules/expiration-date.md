---
appliesTo:
- type: entity
  id: warranty
  facts:
  - Expiration date
  - Warranty period
  - Purchase date
  - Lifetime
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#add_warranty
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_warranty
- kind: code
  role: implementation
  target: backend/warranties_routes.py#import_warranties
---

# A warranty expires at its purchase date plus its warranty period, or on the exact date entered

A warranty that is not lifetime has either a warranty period, whose years, months and days are added to the purchase date to give the expiration date, or an exact expiration date with no period. The expiration date is never before the purchase date, and years never exceed 999. A lifetime warranty has neither.
