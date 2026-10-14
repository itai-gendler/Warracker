---
kind: edge
routes:
  web: Web
steps:
- text: The Admin opens the Apprise notification settings
  kind: actor
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Apprise library is not available
  kind: condition
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
  actor: admin
- text: The Product shows that Apprise notifications are not available
  kind: product
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
references:
- kind: code
  role: implementation
  target: backend/notifications.py#process_apprise_notifications
- kind: code
  role: implementation
  target: backend/notifications.py#filter_to_due_thresholds
- kind: code
  role: implementation
  target: backend/apprise_handler.py
- kind: code
  role: implementation
  target: backend/admin_routes.py#trigger_apprise_expiration_notifications
- kind: code
  role: implementation
  target: backend/migrations/051_add_notification_log.sql
---

# Apprise unavailable

## Trigger

An Admin opens the Apprise settings while the Apprise library is not available on the installation.

## Outcome

The Admin sees that Apprise notifications are not available, and none are sent.
