---
references:
- kind: code
  role: implementation
  target: frontend/settings-new.html
- kind: code
  role: implementation
  target: backend/apprise_handler.py
---

# Apprise notifications

Apprise expiry notifications: their configuration, test notifications, and sending them on schedule or on demand.

## Boundary

Owns notifications sent through Apprise. Does not own email reminders or a person's own notification settings.
