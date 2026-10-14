---
appliesTo:
- type: entity
  id: account
  effect: removes
permits:
- related:
  - verb: identifies
    entity: user
- related:
  - verb: identifies
    entity: admin
- actors:
  - admin
  - owner
  when:
  - fact: Application owner
    is: 'Off'
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#delete_account
- kind: code
  role: implementation
  target: backend/admin_routes.py#delete_user
---

# People delete their own account, admins delete others, and the Owner is never deleted

A User or an Admin deletes their own account from their settings; admins and the Owner delete other accounts from the users list. The Owner's account is never deleted, by anyone, until ownership is transferred.
