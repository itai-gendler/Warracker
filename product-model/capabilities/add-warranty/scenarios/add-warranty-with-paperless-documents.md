---
kind: primary
routes:
  web: Web
steps:
- text: The User enters the warranty's details and chooses Paperless-ngx as the storage for the invoice
  kind: actor
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The Paperless-ngx integration is enabled
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Paperless-ngx enabled
  contexts:
    web:
      place: web::signed-in::add-warranty
  actor: user
- text: The User uploads the invoice file
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The Product uploads the file to Paperless-ngx, then adds the warranty linked to that Paperless-ngx document
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
    - Paperless document
    with: warranty
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
- kind: code
  role: implementation
  target: backend/file_routes.py#paperless_upload
---

# Add a warranty with documents in Paperless-ngx

## Trigger

A User wants their invoice kept in the installation's Paperless-ngx instance.

## Outcome

The warranty is tracked and its invoice lives in Paperless-ngx, linked from the warranty.

## Edge cases

- When the upload to Paperless-ngx fails, the User is told and the document is not linked.
