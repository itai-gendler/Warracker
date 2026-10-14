---
kind: primary
routes:
  web: Web
steps:
- text: The User opens the invoice of one of their warranties
  kind: actor
  actor: user
  entities:
  - entity: document
    effect: reads
    facts:
    - Kind
    - Storage
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::home
- text: The Product opens the stored file
  kind: product
  actor: user
  entities:
  - entity: document
    effect: reads
    facts:
    - File
  contexts:
    web:
      place: web::signed-in::home
references:
- kind: code
  role: implementation
  target: backend/file_routes.py#_check_file_authorization
- kind: code
  role: implementation
  target: backend/file_routes.py#secure_file_access
- kind: code
  role: implementation
  target: backend/file_routes.py#serve_paperless_document
- kind: code
  role: implementation
  target: frontend/js/components/warrantyRenderer.js
---

# Open a document of one's own warranty

## Trigger

A User needs the receipt of one of their warranties.

## Outcome

The document opens.
