---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#logout
---

# Sign out

A signed-in person ends their session and returns to the sign-in page.
