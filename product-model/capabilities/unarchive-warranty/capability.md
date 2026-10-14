---
domain: warranties
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#toggle_archive_warranty
- kind: code
  role: implementation
  target: frontend/js/components/warrantyActions.js
---

# Unarchive warranty

A person brings an archived warranty back to the main list.
