---
appliesTo:
- type: entity
  id: warranty
  facts:
  - Claim summary
- type: entity
  id: claim
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_warranties
---

# A warranty's claims are open while any is Submitted or In Progress

A warranty without claims shows No claims; with any claim Submitted or In Progress it shows Open; otherwise Finished.
