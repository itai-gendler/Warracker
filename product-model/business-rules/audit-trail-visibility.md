---
appliesTo:
- type: entity
  id: audit-trail-entry
  effect: reads
permits:
- actors:
  - admin
  - owner
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_audit_trail
---

# Only admins read the audit trail

The audit trail is read only by admins and the Owner.
