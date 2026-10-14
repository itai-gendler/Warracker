---
kind: primary
routes:
  web: Web
steps:
- text: The User sets their language, theme, default view, currency symbol and position, expiring soon days and date format and saves
  kind: actor
  actor: user
  entities:
  - entity: account
    effect: reads
    facts:
    - Preferred language
    - Theme
    - Default view
    - Currency symbol
    - Currency position
    - Expiring soon days
    - Date format
  contexts:
    web:
      place: web::signed-in::settings
- text: Expiring soon days is between 1 and 365 and the currency symbol has at most 8 characters
  kind: condition
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
  actor: user
- text: The Product saves the preferences to the account
  kind: product
  actor: user
  entities:
  - entity: account
    effect: changes
    facts:
    - Preferred language
    - Theme
    - Default view
    - Currency symbol
    - Currency position
    - Expiring soon days
    - Date format
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_preferences
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change preferences

## Trigger

A User wants Warracker shown their way.

## Outcome

The preferences apply from now on, on every device they sign in from.

## Edge cases

- A language picked anywhere in the interface switches it at once and is saved as the preferred language.
