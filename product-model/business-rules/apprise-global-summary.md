---
appliesTo:
- type: capability
  id: send-apprise-notifications
- type: entity
  id: site-settings
  facts:
  - Apprise notification mode
references:
- kind: code
  role: implementation
  target: backend/notifications.py#process_apprise_notifications
- kind: code
  role: implementation
  target: backend/apprise_handler.py
---

# Apprise sends one summary covering everyone due

In Global Summary mode, each scheduled Apprise run sends, for each number of days left, one notification listing every due warranty of the people whose Apprise notification time it is.
