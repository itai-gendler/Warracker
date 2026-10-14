---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_warranty
- kind: code
  role: implementation
  target: frontend/js/components/warrantyActions.js
---

# Delete warranty

A person permanently deletes a warranty with its documents and claims, from Home or the status dashboard. Admins can delete anyone's warranty.
