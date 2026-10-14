---
appliesTo:
- type: entity
  id: account
  effect: changes
  facts:
  - First name
  - Last name
  - Email
permits:
- related:
  - verb: identifies
    entity: user
  when:
  - fact: Sign-in method
    is: Local
- related:
  - verb: identifies
    entity: admin
  when:
  - fact: Sign-in method
    is: Local
- related:
  - verb: identifies
    entity: owner
  when:
  - fact: Sign-in method
    is: Local
- actors:
  - visitor
  when:
  - fact: Sign-in method
    is: OIDC SSO
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_profile
- kind: code
  role: implementation
  target: frontend/settings-new.js
- kind: code
  role: implementation
  target: backend/oidc_handler.py#oidc_callback_route
---

# People edit their own profile only when they sign in locally

A person with a local account edits their own name and email. An OIDC SSO account's name and email come from the provider and are refreshed at each single sign-on.
