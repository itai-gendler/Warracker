---
availability:
- place: web::public
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#register
- kind: code
  role: implementation
  target: frontend/register.html
---

# Register account

A person creates a local account with a username, email and password and is signed in to Home. Registration exists while the site setting allows it; the first account on an installation is always accepted and becomes its Admin and Owner.
