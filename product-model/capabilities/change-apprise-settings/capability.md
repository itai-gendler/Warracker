---
domain: apprise-notifications
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/admin_routes.py#reload_apprise_configuration
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change Apprise settings

An admin configures Apprise notifications: whether they are enabled, the notification mode, the warranty scope, the destination URLs, the notification days and the message title prefix.
