---
appliesTo:
- type: entity
  id: account
  effect: reads
  facts:
  - Email
  - Last login
permits:
- related:
  - verb: identifies
    entity: user
- related:
  - verb: identifies
    entity: admin
- related:
  - verb: identifies
    entity: owner
- actors:
  - admin
  - owner
- unattended: true
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#get_all_users
---

# Only admins see other people's email and last login

A person sees their own email; admins and the Owner see every account's email and last login in the users list. Reminders use the email of the person they go to.
