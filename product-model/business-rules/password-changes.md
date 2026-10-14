---
appliesTo:
- type: entity
  id: account
  effect: changes
  facts:
  - Password
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
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#change_password
- kind: code
  role: implementation
  target: backend/auth_routes.py#reset_password
---

# A password is changed by its account holder or through a reset link

People with a local account change their own password by giving the current one; a person who follows a valid reset link sets a new one.
