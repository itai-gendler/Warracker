---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#add_warranty
- kind: code
  role: implementation
  target: frontend/js/components/addWarrantyForm.js
- kind: code
  role: implementation
  target: backend/utils.py#allowed_file
---

# Add warranty

A person adds a warranty for a product they bought: its name and purchase date, coverage as a period from the purchase date, an exact expiration date or lifetime, any vendor, model number, serial numbers, type, price, currency, notes and links, its documents and its tags. Documents can be stored in Paperless-ngx while the Paperless-ngx integration is enabled.
