---
appliesTo:
- type: entity
  id: warranty
  facts:
  - Expiry status
- type: entity
  id: account
  facts:
  - Expiring soon days
references:
- kind: code
  role: implementation
  target: frontend/js/lib/warrantyProcessing.js
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_statistics
---

# A warranty is expired after its expiration date and expiring soon within the viewer's expiring soon days

A lifetime warranty never expires. Any other warranty is Expired once its expiration date has passed, Expiring soon while it expires within the viewer's expiring soon days, and Active otherwise; a warranty expiring today is not yet expired.
