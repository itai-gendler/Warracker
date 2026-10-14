---
appliesTo:
- type: entity
  id: account
  effect: changes
  facts:
  - Preferred language
  - Theme
  - Default view
  - Currency symbol
  - Currency position
  - Expiring soon days
  - Date format
  - Notification channel
  - Email notification frequency
  - Email notification time
  - Email timezone
  - Apprise notification time
  - Apprise notification frequency
  - Apprise timezone
  - View Paperless documents in Warracker
  - Saved filters
permits:
- related:
  - verb: identifies
    entity: user
- related:
  - verb: identifies
    entity: admin
- related:
  - verb: identifies
    entity: owner
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_preferences
---

# People change only their own preferences and notification settings

Display preferences, notification settings and saved filters are changed only by the person whose account they belong to.
