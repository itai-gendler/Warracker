---
domain: warranties
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#add_warranty
- kind: code
  role: implementation
  target: backend/file_routes.py
- kind: code
  role: implementation
  target: backend/paperless_handler.py
---

# Document

A file kept with a warranty: its product photo, invoice or receipt, manual, or other files such as a ZIP or RAR archive. A warranty holds at most one of each kind.

## Information kept

- **Kind** — Product photo, Invoice, Manual or Files
- **Storage** — Local, on the Warracker server, or Paperless-ngx, in the connected Paperless-ngx instance
- **File** — the uploaded file, for a locally stored document
- **Paperless document** — the Paperless-ngx document it refers to, for a document stored in Paperless-ngx
