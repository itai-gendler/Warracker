---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Export
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::home
- text: The Product downloads a CSV of the listed warranties that match the current filters, with tags and serial numbers as JSON lists
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
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
    - Expiry status
  - entity: tag
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: frontend/js/components/importExport.js#exportWarranties
---

# Export warranties to CSV

## Trigger

A User wants a copy of their warranty list.

## Outcome

The User has a dated CSV file of the listed warranties, matching the current filters.
