---
entities:
- entity: site-settings
  shows:
  - Registration enabled
  - Email base URL
  - Global view enabled
  - Global view admin only
  - OIDC SSO enabled
  - OIDC-only login mode
  - OIDC provider name
  - Client ID
  - Issuer URL
  - Scope
  - OIDC admin group
  - Paperless-ngx enabled
  - Paperless-ngx URL
  - Apprise enabled
  - Apprise URLs
  - Notification days
  - Apprise notification mode
  - Warranty scope
  - Message title prefix
  collects:
  - Registration enabled
  - Email base URL
  - Global view enabled
  - Global view admin only
  - OIDC SSO enabled
  - OIDC-only login mode
  - OIDC provider name
  - Client ID
  - Client secret
  - Issuer URL
  - Scope
  - OIDC admin group
  - Paperless-ngx enabled
  - Paperless-ngx URL
  - Paperless-ngx API token
  - Apprise enabled
  - Apprise URLs
  - Notification days
  - Apprise notification mode
  - Warranty scope
  - Message title prefix
- entity: account
  shows:
  - View Paperless documents in Warracker
  collects:
  - View Paperless documents in Warracker
references:
- kind: code
  role: implementation
  target: frontend/settings-new.html
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Admin settings

The admin actions, site settings, OIDC SSO configuration, Paperless-ngx integration and Apprise notification settings of the installation.
