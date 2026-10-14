---
kind: edge
routes:
  web: Web
steps:
- text: It is the email notification time of a person with warranties due, and the mail server cannot be reached
  kind: condition
  unattended: true
  entities:
  - entity: account
    effect: reads
    facts:
    - Email notification time
  - entity: warranty
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in
- text: The Product sends nothing for that due time
  kind: product
  entities: []
  contexts:
    web:
      place: web::signed-in
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

# Email server unavailable

## Trigger

It is a person's email notification time but the mail server cannot be reached.

## Outcome

No email reaches the person that day; the next reminder goes out at their next due time.
