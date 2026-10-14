---
kind: primary
routes:
  web: Web
steps:
- text: The Admin chooses Send Test Notification, optionally with a test URL
  kind: actor
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product sends a test notification to the test URL, or to the Apprise destinations
  kind: product
  actor: admin
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Apprise URLs
    - Message title prefix
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product reports that the test notification was sent
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

# Send a test notification

## Trigger

An Admin wants to check the Apprise destinations work.

## Outcome

The test notification arrives and the Admin is told it was sent.
