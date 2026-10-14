---
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change site settings

An admin changes the site settings: whether registration is enabled, the email base URL, whether the global view is enabled, and whether it is limited to admins.
