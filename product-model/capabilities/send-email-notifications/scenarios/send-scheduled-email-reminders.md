---
kind: primary
routes:
  web: Web
steps:
- text: It is the email notification time of an active person whose channel is Email or Both, on a day their frequency includes
  kind: condition
  unattended: true
  entities:
  - entity: account
    effect: reads
    facts:
    - Active status
    - Notification channel
    - Email notification frequency
    - Email notification time
    - Email timezone
  contexts:
    web:
      place: web::signed-in
- text: The Product collects the person's tracked warranties that are not lifetime and expire from today through their expiring soon days
  kind: product
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Expiration date
    - Lifetime
  - entity: account
    effect: reads
    facts:
    - Expiring soon days
  contexts:
    web:
      place: web::signed-in
- text: The Product emails the person the product names and expiration dates with links to Warracker and to the notification settings
  kind: product
  entities:
  - entity: account
    effect: reads
    facts:
    - Email
    - First name
  - entity: site-settings
    effect: reads
    facts:
    - Email base URL
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

# Send scheduled email reminders

## Trigger

It is a person's email notification time in their timezone, on a day their frequency includes: every day, Mondays, or the 1st of the month.

## Outcome

The person has an email listing their warranties that expire within their expiring soon days, with links to Warracker and to their notification settings.

## Edge cases

- No email is sent when none of the person's warranties is due.
- The same warranties are listed again on every due day until they expire.
- Each person gets at most one scheduled email reminder a day.
