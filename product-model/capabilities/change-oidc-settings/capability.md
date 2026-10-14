---
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/oidc_handler.py#init_oidc_client
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change OIDC settings

An admin configures OIDC single sign-on: whether it is enabled, OIDC-only login mode, the provider name, client ID and secret, issuer URL, scope and admin group.
