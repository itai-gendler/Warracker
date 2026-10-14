---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_preferences
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change preferences

A person changes their preferences: language, light or dark theme, default view, currency symbol and position, expiring soon days and date format.
