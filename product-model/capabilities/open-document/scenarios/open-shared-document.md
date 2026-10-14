---
kind: primary
routes:
  web: Web
steps:
- text: The User opens the manual of a warranty someone else added, in the global scope
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
- text: The global view is enabled and not restricted to administrators, and the document is a photo, invoice or manual
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Global view enabled
    - Global view admin only
  - entity: document
    effect: reads
    facts:
    - Kind
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product opens the document
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

# Open the document of someone else's warranty

## Trigger

A User browsing the global scope wants to see the manual of a product someone else added.

## Outcome

The manual opens, read-only.
