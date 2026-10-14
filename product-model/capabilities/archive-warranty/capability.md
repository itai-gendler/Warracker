---
domain: warranties
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#toggle_archive_warranty
- kind: code
  role: implementation
  target: frontend/js/components/warrantyActions.js
---

# Archive warranty

A person sets a warranty aside on the archived list, keeping everything it holds while it leaves the main list, the dashboard counts and scheduled reminders. Admins can archive anyone's warranty.
