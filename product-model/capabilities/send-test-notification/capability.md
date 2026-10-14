---
domain: apprise-notifications
availability:
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#test_apprise_notification
- kind: code
  role: implementation
  target: backend/apprise_handler.py
---

# Send test notification

An admin sends a test Apprise notification to a test URL, or to the configured destinations when none is given.
