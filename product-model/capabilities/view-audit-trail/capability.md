---
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_audit_trail
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# View audit trail

An admin reads the most recent recorded administrative changes, newest first.
