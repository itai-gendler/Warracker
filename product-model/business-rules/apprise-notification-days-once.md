---
appliesTo:
- type: capability
  id: send-apprise-notifications
- type: entity
  id: site-settings
  facts:
  - Notification days
references:
- kind: code
  role: implementation
  target: backend/notifications.py#filter_to_due_thresholds
- kind: code
  role: implementation
  target: backend/notifications.py#mark_thresholds_sent
- kind: code
  role: implementation
  target: backend/migrations/051_add_notification_log.sql
---

# Each Apprise notification day is notified once per warranty

A scheduled Apprise notification covers a warranty when the days left to its expiry have fallen to one of the notification days and that notification day has not been notified for it yet; it is then marked notified and not repeated.
