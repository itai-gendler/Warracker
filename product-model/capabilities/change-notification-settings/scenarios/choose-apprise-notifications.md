---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Apprise or Both, a time of day and a timezone and saves
  kind: actor
  actor: user
  entities:
  - entity: account
    effect: reads
    facts:
    - Notification channel
    - Email notification frequency
    - Email notification time
    - Email timezone
    - Apprise notification time
    - Apprise notification frequency
    - Apprise timezone
  contexts:
    web:
      place: web::signed-in::settings
- text: The Product saves the notification settings to the account
  kind: product
  actor: user
  entities:
  - entity: account
    effect: changes
    facts:
    - Notification channel
    - Apprise notification time
    - Apprise notification frequency
    - Apprise timezone
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_preferences
- kind: code
  role: implementation
  target: frontend/settings-new.html
---

# Choose Apprise notifications

## Trigger

A User wants their expiring warranties included in Apprise notifications.

## Outcome

The User's warranties join Apprise notifications at the chosen local time.
