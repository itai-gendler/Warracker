---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_statistics
- kind: code
  role: implementation
  target: frontend/status.js
---

# View status dashboard

A person reads the status of their own warranties: how many are active, expiring soon, expired and archived, their total purchase value, the status distribution, the expiration timeline for the next 90 days, and the warranties recently expired or expiring soon.
