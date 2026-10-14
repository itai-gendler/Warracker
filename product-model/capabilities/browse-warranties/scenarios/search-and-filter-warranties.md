---
kind: primary
routes:
  web: Web
steps:
- text: The User types a search term, picks an expiry status, tag, vendor or warranty type, and a sort order
  kind: actor
  actor: user
  entities:
  - entity: tag
    effect: reads
    facts:
    - Name
  - entity: warranty
    effect: reads
    facts:
    - Vendor
  contexts:
    web:
      place: web::signed-in::home
- text: The Product lists the warranties matching every choice in that order
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Model number
    - Vendor
    - Notes
    - Tags
    - Serial numbers
    - Expiry status
    - Warranty type
  contexts:
    web:
      place: web::signed-in::home
- text: The Product saves the choices to the account
  kind: product
  actor: user
  entities:
  - entity: account
    effect: changes
    facts:
    - Saved filters
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_warranties
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_archived_warranties
- kind: code
  role: implementation
  target: frontend/js/controllers/warrantyListController.js
- kind: code
  role: implementation
  target: frontend/js/lib/warrantyProcessing.js
---

# Search and filter warranties

## Trigger

A User looks for particular warranties among their own.

## Outcome

Only the matching warranties are listed in the chosen order, and the choices are remembered for the next visit.
