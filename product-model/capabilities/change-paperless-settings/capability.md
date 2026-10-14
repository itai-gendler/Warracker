---
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/paperless_handler.py#get_paperless_handler
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change Paperless-ngx settings

An admin enables or disables the Paperless-ngx integration and sets the instance URL and API token.
