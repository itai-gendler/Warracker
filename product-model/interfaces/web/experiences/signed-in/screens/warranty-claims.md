---
entities:
- entity: warranty
  shows:
  - Product name
- entity: claim
  shows:
  - Claim date
  - Claim number
  - Description
  - Resolution
  - Resolution date
  collects:
  - Claim date
  - Claim number
  - Description
  - Resolution
  - Resolution date
references:
- kind: code
  role: implementation
  target: frontend/js/components/claims.js
---

# Warranty claims

The claims of one warranty, newest claim date first, with each claim's status, and the form for adding or editing a claim.
