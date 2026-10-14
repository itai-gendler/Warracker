---
references:
- kind: code
  role: implementation
  target: backend/audit_logger.py#create_audit_log
- kind: code
  role: implementation
  target: backend/migrations/048_create_audit_log_table.sql
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_audit_trail
---

# Audit trail entry

One recorded administrative change, shown to admins in the audit trail.

## Information kept

- **Timestamp** — when the change was made
- **User** — who made it
- **Action** — what kind of change it was: a user update, a user deletion or a setting update
- **Details** — what changed; secret values appear masked
- **IP address** — the address the change came from
