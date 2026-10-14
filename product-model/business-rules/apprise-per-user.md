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

# Apprise sends each person's due warranties separately

In Per User mode, each scheduled Apprise run sends each due person's warranties as notifications of their own, grouped by days left, to the same Apprise destinations.
