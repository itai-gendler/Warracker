---
kind: validation
routes:
  web: Web
steps:
- text: The User looks at a warranty someone else added, in the global scope
  kind: actor
  actor: user
  entities:
  - entity: document
    effect: reads
    facts:
    - Kind
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::home
- text: The document is of the Files kind
  kind: condition
  entities:
  - entity: document
    effect: reads
    facts:
    - Kind
  contexts:
    web:
      place: web::signed-in::home
  actor: user
- text: The Product offers no link to the files and refuses them if requested
  kind: product
  actor: user
  entities: []
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

# Files of someone else's warranty

## Trigger

A User browsing the global scope looks for the other files of a warranty someone else added.

## Outcome

The files are not offered, and requesting them is refused.
