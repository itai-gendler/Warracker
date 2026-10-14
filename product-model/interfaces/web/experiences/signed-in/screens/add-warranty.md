---
entities:
- entity: warranty
  collects:
  - Product name
  - Purchase date
  - Lifetime
  - Warranty period
  - Expiration date
  - Warranty type
  - Vendor
  - Model number
  - Serial numbers
  - Product URL
  - Purchase price
  - Currency
  - Notes
  - Invoice URL
  - Manual URL
  - Files URL
  - Tags
- entity: document
  collects:
  - Kind
  - Storage
  - File
  - Paperless document
- entity: tag
  shows:
  - Name
  - Color
references:
- kind: code
  role: implementation
  target: frontend/js/components/addWarrantyForm.js
- kind: code
  role: implementation
  target: frontend/index.html
---

# Add warranty

The process of adding a warranty: product information, warranty details, documents, tags, and a summary to check before adding it.
