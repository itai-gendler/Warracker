---
entities:
- entity: account
  collects:
  - Username
  - Email
  - Password
  - First name
  - Last name
- entity: site-settings
  shows:
  - Registration enabled
entryPoints:
- web: /register.html
references:
- kind: code
  role: implementation
  target: frontend/register.html
---

# Registration

Where a person creates an account while registration is enabled.
