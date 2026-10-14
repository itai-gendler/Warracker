---
kind: primary
routes:
  web: Web
steps:
- text: The Admin enters the OIDC SSO settings and saves, leaving the client secret blank to keep the stored one
  kind: actor
  actor: admin
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - OIDC SSO enabled
    - OIDC-only login mode
    - OIDC provider name
    - Client ID
    - Issuer URL
    - Scope
    - OIDC admin group
  contexts:
    web:
      place: web::administration::admin-settings
- text: The Product saves the settings and applies the new single sign-on configuration
  kind: product
  actor: admin
  entities:
  - entity: site-settings
    effect: changes
    facts:
    - OIDC SSO enabled
    - OIDC-only login mode
    - OIDC provider name
    - Client ID
    - Client secret
    - Issuer URL
    - Scope
    - OIDC admin group
  contexts:
    web:
      place: web::administration::admin-settings
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/oidc_handler.py#init_oidc_client
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Change OIDC settings

## Trigger

An Admin connects the installation to the household's or team's identity provider.

## Outcome

The OIDC settings are saved and single sign-on is configured again with them; each change is in the audit trail.

## Edge cases

- When the new configuration cannot be applied, the Admin is told a restart may be needed.
- Single sign-on stays off until a client ID, client secret and issuer URL are all set.
