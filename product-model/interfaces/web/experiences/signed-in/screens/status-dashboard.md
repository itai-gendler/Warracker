---
entities:
- entity: warranty
  shows:
  - Product name
  - Purchase date
  - Expiration date
  - Expiry status
  - Purchase price
  - Archived at
- entity: account
  shows:
  - First name
  - Last name
  - Username
  - Expiring soon days
entryPoints:
- web: /status.html
references:
- kind: code
  role: implementation
  target: frontend/status.html
- kind: code
  role: implementation
  target: frontend/status.js
- kind: code
  role: implementation
  target: backend/statistics_routes.py
---

# Status dashboard

Counts of active, expiring soon, expired, archived and all warranties with their total purchase value, the status distribution, the expiration timeline for the next 90 days, and the warranties recently expired or expiring soon, for the person's own warranties or, in the global scope, everyone's.
