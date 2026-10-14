---
singleton: true
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_site_settings
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_site_settings
- kind: code
  role: implementation
  target: backend/oidc_handler.py#init_oidc_client
- kind: code
  role: implementation
  target: backend/apprise_handler.py
- kind: code
  role: implementation
  target: backend/paperless_handler.py#get_paperless_handler
---

# Site settings

The installation-wide settings admins manage. Where the deployment environment sets the same value (OIDC SSO, Apprise and the email base URL), the environment value takes precedence over the stored one.

## Information kept

- **Registration enabled** — whether new accounts may be created; on unless changed
- **Email base URL** — the address used for links in emails
- **Global view enabled** — whether signed-in people may browse everyone's warranties read-only; on unless changed
- **Global view admin only** — whether the global view is limited to admins; off unless changed
- **OIDC SSO enabled** — whether people may sign in through the OIDC single sign-on provider
- **OIDC-only login mode** — whether people sign in only through single sign-on
- **OIDC provider name** — the provider name shown on the sign-in button
- **Client ID** — the client the installation is registered as at the provider
- **Client secret** — the client secret, write-only: admins see only whether it is set
- **Issuer URL** — the provider's issuer address
- **Scope** — the scopes requested from the provider
- **OIDC admin group** — the provider group whose members hold admin rights
- **Paperless-ngx enabled** — whether people may store documents in Paperless-ngx
- **Paperless-ngx URL** — the Paperless-ngx instance's address
- **Paperless-ngx API token** — the token used to reach Paperless-ngx, write-only
- **Apprise enabled** — whether Apprise notifications are sent
- **Apprise URLs** — the Apprise destinations notifications are sent to
- **Notification days** — how many days before expiry Apprise notifies, 7 and 30 unless changed
- **Apprise notification mode** — Global Summary or Per User
- **Warranty scope** — whether Apprise notifications cover all users' warranties or only the admin's
- **Message title prefix** — the prefix of Apprise notification titles, [Warracker] unless changed
