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
  target: backend/admin_routes.py#transfer_ownership
- kind: code
  role: implementation
  target: backend/__init__.py#ensure_owner_exists
---

# Owner

The one application owner: an admin whose account can never be demoted, deactivated or deleted, and who alone can hand ownership to another admin.
