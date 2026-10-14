---
appliesTo:
- type: entity
  id: account
  effect: creates
permits:
- actors:
  - visitor
  when:
  - entity: site-settings
    fact: Registration enabled
    is: 'On'
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#register
- kind: code
  role: implementation
  target: backend/oidc_handler.py#oidc_callback_route
---

# Accounts are created only while registration is enabled

A new account, by registering or by signing in with single sign-on for the first time, is created only while registration is enabled. The very first account of an installation is accepted whatever the setting.
