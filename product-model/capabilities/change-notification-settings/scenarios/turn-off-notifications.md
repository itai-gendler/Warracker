---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses Disabled and saves
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
- text: The Product saves the notification channel to the account
  kind: product
  actor: user
  entities:
  - entity: account
    effect: changes
    facts:
    - Notification channel
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

# Turn off notifications

## Trigger

A User wants no expiry reminders.

## Outcome

No scheduled reminder covers the User's warranties.
