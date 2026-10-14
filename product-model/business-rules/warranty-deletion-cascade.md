---
appliesTo:
- type: entity
  id: warranty
  effect: removes
- type: entity
  id: claim
- type: entity
  id: document
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_warranty
- kind: code
  role: implementation
  target: backend/migrations/044_create_warranty_claims_table.sql
---

# Deleting a warranty deletes its documents and claims

When a warranty is deleted, alone or with its account, its documents, their stored files and its claims are deleted with it.
