---
appliesTo:
- type: capability
  id: edit-user
- type: capability
  id: delete-user
- type: capability
  id: change-site-settings
- type: capability
  id: change-oidc-settings
- type: capability
  id: change-paperless-settings
- type: capability
  id: change-apprise-settings
- type: entity
  id: audit-trail-entry
references:
- kind: code
  role: implementation
  target: backend/audit_logger.py#create_audit_log
- kind: code
  role: implementation
  target: backend/admin_routes.py
---

# Changes to accounts and site settings by admins are recorded in the audit trail

Every change an admin makes to another account's admin or active status, every account an admin deletes, and every site setting saved, single sign-on, Paperless-ngx and Apprise settings included, is recorded with who made it, when, from where and what changed; secret values are masked.
