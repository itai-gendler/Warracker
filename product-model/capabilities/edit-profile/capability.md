---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_profile
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Edit profile

A person with a local account changes their first name, last name and email in the account settings. An OIDC SSO account shows its profile read-only, kept by the provider.
