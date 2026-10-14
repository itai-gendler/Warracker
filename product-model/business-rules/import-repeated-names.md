---
appliesTo:
- type: capability
  id: import-warranties
- type: entity
  id: warranty
  facts:
  - Product name
  - Purchase date
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#import_warranties
---

# An imported warranty repeating a product name and purchase date gets a numbered name

When an imported row has the same product name and purchase date as one of the person's warranties, or as an earlier row of the same file, it is imported with the first free suffix " (1)", " (2)" and so on, rather than refused.
