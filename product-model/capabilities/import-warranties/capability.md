---
domain: warranties
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#import_warranties
- kind: code
  role: implementation
  target: frontend/js/components/importExport.js#handleImport
- kind: doc
  role: intent
  target: README.md
---

# Import warranties

A person imports warranties from a CSV file with a ProductName and PurchaseDate column and optional coverage, price, currency, serial number, URL, tag, vendor, type, notes and model number columns. Valid rows are added even when others fail, unknown tags are created, and every failed row is reported with its reasons.
