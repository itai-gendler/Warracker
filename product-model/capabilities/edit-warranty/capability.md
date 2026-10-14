---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_warranty
- kind: code
  role: implementation
  target: frontend/js/components/editModal.js
- kind: code
  role: implementation
  target: frontend/js/components/notes.js
---

# Edit warranty

A person changes a warranty's details, coverage, notes, links and documents, from Home or the status dashboard. Admins can edit anyone's warranty.
