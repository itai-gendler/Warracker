---
appliesTo:
- type: entity
  id: warranty
  facts:
  - Archived at
- type: capability
  id: send-email-notifications
- type: capability
  id: view-status-dashboard
references:
- kind: code
  role: implementation
  target: backend/notifications.py#get_expiring_warranties
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_statistics
---

# Archived warranties leave the main list, the dashboard counts and scheduled reminders

An archived warranty keeps everything it holds but is listed only on the archived list, counted only as Archived on the status dashboard and left out of its total value, and never included in scheduled reminders.
