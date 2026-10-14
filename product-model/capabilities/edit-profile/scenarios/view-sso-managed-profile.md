---
kind: validation
routes:
  web: Web
steps:
- text: The User opens the account settings
  kind: actor
  actor: user
  entities:
  - entity: account
    effect: reads
    facts:
    - Sign-in method
    - First name
    - Last name
    - Email
  contexts:
    web:
      place: web::signed-in::settings
- text: The account signs in with OIDC SSO
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::settings
  actor: user
- text: The Product shows the profile as managed by the provider, without offering to save it or to change the password
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_profile
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# View a profile managed by single sign-on

## Trigger

A User signed in with an OIDC SSO account opens the account settings.

## Outcome

The name and email are shown read-only as managed by the provider, and the security section with password change is not offered.
