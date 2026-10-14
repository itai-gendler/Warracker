---
domain: warranties
availability:
- place: web::signed-in
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

# Open document

A person opens a document kept with a warranty: its product photo, invoice, manual or files. People other than the one who added the warranty open only its photo, invoice and manual, and only through the global view; admins open any document.
