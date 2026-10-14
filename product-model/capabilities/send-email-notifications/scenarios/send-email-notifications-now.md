---
kind: primary
routes:
  web: Web
steps:
- text: The Admin chooses to send the email notifications now
  kind: actor
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product emails every active person whose channel is Email or Both their tracked warranties expiring within their expiring soon days
  kind: product
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts:
    - Active status
    - Notification channel
    - Expiring soon days
    - Email
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Expiration date
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product confirms that the notifications were triggered
  kind: product
  actor: admin
  entities: []
  contexts:
    web:
      place: web::administration::admin-settings
references:
- kind: code
  role: implementation
  target: backend/notifications.py#send_expiration_notifications
- kind: code
  role: implementation
  target: backend/notifications.py#get_expiring_warranties
- kind: code
  role: implementation
  target: backend/notifications.py#is_notification_due
- kind: code
  role: implementation
  target: backend/notifications.py#format_expiration_email
- kind: code
  role: implementation
  target: backend/admin_routes.py#trigger_notifications
---

# Send email notifications now

## Trigger

An Admin chooses Send Warranty Notifications in the admin actions.

## Outcome

Every active person whose channel is Email or Both gets their email at once, whatever their time and frequency.

## Edge cases

- A person emailed within the last two minutes is skipped.
- Apprise notifications are not part of this run.
