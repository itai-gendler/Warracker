---
kind: configuration
of: business-rule
settings:
- entity: site-settings
  fact: Apprise notification mode
takesEffect: At each scheduled Apprise run; a change applies from the next run.
stability: Notifications already sent are not resent; the notification days already marked notified stay marked whichever mode sent them.
alternatives:
- id: apprise-global-summary
  selectedWhen: Notification Mode is Global Summary. A missing mode uses Global Summary.
- id: apprise-per-user
  selectedWhen: Notification Mode is Per User.
references:
- kind: code
  role: implementation
  target: backend/notifications.py#process_apprise_notifications
- kind: code
  role: implementation
  target: backend/migrations/032_add_apprise_notification_mode.sql
---

# Apprise notification mode

Admins choose whether scheduled Apprise notifications summarize everyone's due warranties together or send each person's separately; both policies are supported.
