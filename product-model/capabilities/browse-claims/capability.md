---
domain: warranties
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_claims
- kind: code
  role: implementation
  target: backend/warranties_routes.py#create_claim
- kind: code
  role: implementation
  target: backend/warranties_routes.py#update_claim
- kind: code
  role: implementation
  target: backend/warranties_routes.py#delete_claim
- kind: code
  role: implementation
  target: frontend/js/components/claims.js
---

# Browse claims

A person opens a warranty's claims to see each claim's date, status, number, description and resolution, newest claim date first. Other people's claims are readable through the global view.
