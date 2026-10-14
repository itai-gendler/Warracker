---
appliesTo:
- type: entity
  id: site-settings
  effect: changes
permits:
- actors:
  - admin
  - owner
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/auth_utils.py#admin_required
---

# Only admins change the site settings

Site settings, single sign-on, Paperless-ngx and Apprise settings are changed only by admins and the Owner. Secret values are never shown back, and saving one blank keeps the stored value.
