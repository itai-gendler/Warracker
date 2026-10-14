---
type: web
actors:
- visitor
- user
- admin
- owner
entryPoints:
- web: /
- web: /login.html
- web: /register.html
- web: /reset-password.html
references:
- kind: code
  role: implementation
  target: frontend/index.html
- kind: code
  role: implementation
  target: nginx.conf
- kind: code
  role: implementation
  target: backend/__init__.py#create_app
---

# Web app

The Warracker web app, served by the self-hosted installation, where people sign in, keep their warranties and adjust their settings, and admins administer the installation.
