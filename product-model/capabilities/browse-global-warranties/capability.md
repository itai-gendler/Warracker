---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_global_warranties
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_global_warranties_archived
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_global_statistics
- kind: code
  role: implementation
  target: frontend/js/components/warrantyRenderer.js
---

# Browse global warranties

While the global view is enabled, a signed-in person switches the scope of Home or the status dashboard from their own warranties to everyone's, each with the name of the person who added it. Other people's warranties are read-only for everyone but admins. An admin can limit the global view to admins.
