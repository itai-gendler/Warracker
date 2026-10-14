---
kind: primary
routes:
  web: Web
steps:
- text: The User opens the invoice of a warranty, stored in Paperless-ngx
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
- text: The Product opens the Paperless-ngx document
  kind: product
  actor: user
  entities:
  - entity: document
    effect: reads
    facts:
    - Paperless document
  - entity: account
    effect: reads
    facts:
    - View Paperless documents in Warracker
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

# Open a document stored in Paperless-ngx

## Trigger

A User opens an invoice stored in Paperless-ngx.

## Outcome

The Paperless-ngx document opens.

## Decision points

### Where it opens

Does the User view Paperless documents in Warracker?

- Yes → the Product fetches the document from Paperless-ngx and shows it inside Warracker.
- No → the Product opens the document in the Paperless-ngx instance.
