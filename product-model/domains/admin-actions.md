---
references:
- kind: code
  role: implementation
  target: frontend/settings-new.html
---

# Admin actions

The admin actions of the admin settings: the users list, where admins change and delete accounts, and sending warranty notifications on demand.

## Boundary

Owns administering accounts and the on-demand email notification run. Does not own the site settings, single sign-on, Paperless-ngx or Apprise configuration, or ownership transfer.
