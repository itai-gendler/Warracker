---
kind: edge
routes:
  web: Web
steps:
- text: The Admin chooses Send Test Notification
  kind: actor
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
- text: The destination does not accept the notification
  kind: condition
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
  actor: admin
- text: The Product reports that the test notification failed
  kind: product
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#test_apprise_notification
- kind: code
  role: implementation
  target: backend/apprise_handler.py
---

# Test notification fails

## Trigger

An Admin sends a test notification to a destination that does not accept it.

## Outcome

The Admin is told the test notification failed.
