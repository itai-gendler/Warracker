---
domain: warranties
references:
- kind: code
  role: implementation
  target: backend/tags_routes.py
- kind: code
  role: implementation
  target: backend/migrations/020_add_user_id_to_tags.sql
---

# Tag

A person's own label for grouping and filtering their warranties.

## Information kept

- **Name** — at most 50 characters, unique among the person's tags
- **Color** — a hex color shown with the tag
