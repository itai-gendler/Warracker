---
entities:
- entity: warranty
  shows:
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
  shows:
  - Kind
  - Storage
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
  target: frontend/js/components/editModal.js
- kind: code
  role: implementation
  target: frontend/status.html
---

# Warranty editor

One warranty open for editing, from Home or the status dashboard: its product information, warranty details, documents and tags.
