---
entities:
- entity: account
  shows:
  - Username
  - Email
  - First name
  - Last name
  - Sign-in method
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
  collects:
  - First name
  - Last name
  - Email
  - Password
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
entryPoints:
- web: /settings-new.html
references:
- kind: code
  role: implementation
  target: frontend/settings-new.html
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Settings

The person's own settings: account settings, preferences, notification settings, security and the danger zone.
