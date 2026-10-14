---
appliesTo:
- type: entity
  id: document
  effect: creates
- type: capability
  id: add-warranty
references:
- kind: code
  role: implementation
  target: backend/utils.py#allowed_file
- kind: code
  role: implementation
  target: backend/config.py
- kind: code
  role: implementation
  target: backend/__init__.py#create_app
---

# Documents are limited by kind, file type and upload size

A warranty holds at most one document of each kind. Invoices, manuals and files are PDF, PNG, JPG, JPEG, WEBP, GIF, ZIP or RAR files; product photos are PNG, JPG, JPEG, WEBP or GIF images. An upload above the installation's limit, 32 MB unless the deployment sets another, is refused.
