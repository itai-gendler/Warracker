---
entities:
- entity: account
  collects:
  - Email
  - Password
entryPoints:
- web: /reset-password-request.html
- web: /reset-password.html
references:
- kind: code
  role: implementation
  target: frontend/reset-password-request.html
- kind: code
  role: implementation
  target: frontend/reset-password.html
---

# Password reset

Where a person asks for a password reset link and, following the emailed link, chooses a new password.
