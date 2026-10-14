---
kind: primary
routes:
  web: Web
steps:
- text: The Admin enables Apprise, chooses the notification mode and scope, enters destination URLs, notification days and a title prefix, and saves
  kind: actor
  actor: admin
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Apprise enabled
    - Apprise URLs
    - Notification days
    - Apprise notification mode
    - Warranty scope
    - Message title prefix
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product saves the Apprise settings and reloads the Apprise configuration
  kind: product
  actor: admin
  entities:
  - entity: site-settings
    effect: changes
    facts:
    - Apprise enabled
    - Apprise URLs
    - Notification days
    - Apprise notification mode
    - Warranty scope
    - Message title prefix
  contexts:
    web:
      place: web::administration::admin-settings
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/admin_routes.py#reload_apprise_configuration
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change Apprise settings

## Trigger

An Admin wants expiry alerts in the household's chat.

## Outcome

Apprise notifications use the new settings from the next run; each change is in the audit trail.
