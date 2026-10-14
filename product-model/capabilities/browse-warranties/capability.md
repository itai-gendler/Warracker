---
domain: warranties
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_warranties
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_archived_warranties
- kind: code
  role: implementation
  target: frontend/js/controllers/warrantyListController.js
- kind: code
  role: implementation
  target: frontend/js/lib/warrantyProcessing.js
---

# Browse warranties

A person browses their own warranties on Home: the main list or the archived list, searched by product name, model number, vendor, notes, tag or serial number, filtered by expiry status, tag, vendor and warranty type, sorted, and shown as a grid, a list or a table. The filters and sort they choose are remembered for their next visit.
