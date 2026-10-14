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
  target: backend/auth_utils.py#token_required
---

# User

A signed-in person without admin rights. A User keeps and manages their own warranties, documents, claims and tags, and their own settings.
