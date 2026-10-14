---
entities:
- entity: audit-trail-entry
  shows:
  - Timestamp
  - User
  - Action
  - Details
references:
- kind: code
  role: implementation
  target: frontend/settings-new.html
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_audit_trail
---

# Audit trail

The most recent recorded administrative changes, newest first.
