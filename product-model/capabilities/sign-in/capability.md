---
availability:
- place: web::public
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#login
- kind: code
  role: implementation
  target: backend/oidc_handler.py#oidc_callback_route
- kind: code
  role: implementation
  target: frontend/login.html
---

# Sign in

A person signs in with their username or email and password, or through the OIDC single sign-on provider while OIDC SSO is enabled, and lands on Home. Signing in with SSO for the first time creates an OIDC SSO account. In OIDC-only login mode people sign in through single sign-on.
