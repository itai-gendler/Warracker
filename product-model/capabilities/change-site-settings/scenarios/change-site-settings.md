---
kind: primary
routes:
  web: Web
steps:
- text: The Admin sets registration, the email base URL, the global view and whether it is admin only, and saves
  kind: actor
  actor: admin
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Registration enabled
    - Email base URL
    - Global view enabled
    - Global view admin only
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product saves the site settings
  kind: product
  actor: admin
  entities:
  - entity: site-settings
    effect: changes
    facts:
    - Registration enabled
    - Email base URL
    - Global view enabled
    - Global view admin only
  contexts:
    web:
      place: web::administration::admin-settings
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change site settings

## Trigger

An Admin wants to close registration or limit the global view.

## Outcome

The site settings apply at once and each changed setting is in the audit trail.
