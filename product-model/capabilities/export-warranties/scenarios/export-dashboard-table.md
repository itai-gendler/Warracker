---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Export on the status dashboard
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::status-dashboard
- text: The Product downloads a CSV of the warranties shown in the table, with tags and serial numbers as JSON lists
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
      place: web::signed-in::status-dashboard
references:
- kind: code
  role: implementation
  target: frontend/status.js#exportStatusCSV
---

# Export the status dashboard's table

## Trigger

A User wants the dashboard's table as a file.

## Outcome

The User has a CSV file of the warranties shown in the dashboard table, in the same columns.
