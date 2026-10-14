---
kind: primary
routes:
  web: Web
steps:
- text: The Admin enables the integration, enters the Paperless-ngx URL and API token, chooses whether Paperless-ngx files open inside Warracker, and saves
  kind: actor
  actor: admin
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Paperless-ngx enabled
    - Paperless-ngx URL
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product saves the Paperless-ngx settings, and the viewing choice to the account
  kind: product
  actor: admin
  entities:
  - entity: site-settings
    effect: changes
    facts:
    - Paperless-ngx enabled
    - Paperless-ngx URL
    - Paperless-ngx API token
  - entity: account
    effect: changes
    facts:
    - View Paperless documents in Warracker
  contexts:
    web:
      place: web::administration::admin-settings
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/paperless_handler.py#get_paperless_handler
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change Paperless-ngx settings

## Trigger

An Admin connects the installation to the household's Paperless-ngx instance.

## Outcome

People can choose Paperless-ngx as the storage of their documents; the change is in the audit trail.

## Edge cases

- Leaving the API token blank keeps the stored token.
- The integration counts as configured only when both URL and token are set.
