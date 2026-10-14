---
kind: person
acts: external
relations:
- entity: account
  verb: identifies
  cardinality: one-to-one
- entity: warranty
  verb: owns
  cardinality: one-to-many
- entity: tag
  verb: owns
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: backend/auth_utils.py#admin_required
- kind: code
  role: implementation
  target: backend/admin_routes.py
---

# Admin

A signed-in person whose account has admin status. Besides everything a User does, an Admin manages accounts, the site settings, single sign-on, Paperless-ngx and Apprise, reads the audit trail, and may change, archive or delete anyone's warranty.
