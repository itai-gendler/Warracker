---
entities:
- entity: account
  collects:
  - Username
  - Password
- entity: site-settings
  shows:
  - OIDC SSO enabled
  - OIDC-only login mode
  - OIDC provider name
  - Registration enabled
entryPoints:
- web: /login.html
references:
- kind: code
  role: implementation
  target: frontend/login.html
---

# Sign in

Where a person signs in with their username or email and password, or with the single sign-on provider when it is enabled.
