---
appliesTo:
- type: entity
  id: account
  effect: changes
  facts:
  - Admin status
  - Active status
permits:
- actors:
  - admin
  - owner
  when:
  - fact: Application owner
    is: 'Off'
- actors:
  - visitor
  when:
  - fact: Sign-in method
    is: OIDC SSO
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#update_user
- kind: code
  role: implementation
  target: backend/oidc_handler.py#oidc_callback_route
---

# Admins change other people's admin and active status, never the Owner's

Admins and the Owner give or remove admin status and activate or deactivate other accounts. The Owner's account is never demoted or deactivated, and admins do not change their own status from the users list. With an OIDC admin group configured, single sign-on sets an OIDC SSO account's admin status from the provider's groups.
