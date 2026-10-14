---
appliesTo:
- type: capability
  id: import-warranties
- type: entity
  id: warranty
  effect: creates
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#import_warranties
---

# An import keeps every valid row and reports the others

An import adds every valid row even when others fail, and reports each failed row with its reasons; only when every row fails is nothing imported.
