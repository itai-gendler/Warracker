---
appliesTo:
- type: entity
  id: account
  facts:
  - Password
- type: capability
  id: register-account
references:
- kind: code
  role: implementation
  target: backend/auth_utils.py#is_valid_password
- kind: code
  role: implementation
  target: backend/auth_utils.py#is_password_too_long
---

# Passwords have at least 8 characters with upper-case, lower-case and a digit

Every password set by registration, reset or change has at least 8 characters, at least one upper-case letter, one lower-case letter and one digit, and at most 72 bytes.
