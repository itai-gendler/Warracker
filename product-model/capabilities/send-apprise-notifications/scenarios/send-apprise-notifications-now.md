---
kind: primary
routes:
  web: Web
steps:
- text: The Admin chooses Send Expiration Notifications Now
  kind: actor
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
- text: Apprise is enabled with destinations
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Apprise enabled
    - Apprise URLs
  contexts:
    web:
      place: web::administration::admin-settings
  actor: admin
- text: The Product sends, for each notification day, one notification listing the warranties that are not lifetime and expire within that many days, keeping to the warranty scope
  kind: product
  actor: admin
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Expiration date
    - Lifetime
  - entity: site-settings
    effect: reads
    facts:
    - Notification days
    - Warranty scope
    - Message title prefix
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product reports how many notifications were sent and how many failed
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

# Send expiration notifications now

## Trigger

An Admin chooses Send Expiration Notifications Now in the Apprise settings.

## Outcome

The Apprise destinations receive, for each notification day, a notification listing the warranties expiring within that many days, and the Admin sees how many were sent.

## Edge cases

- This run does not consult people's notification settings or mark notification days as notified.
