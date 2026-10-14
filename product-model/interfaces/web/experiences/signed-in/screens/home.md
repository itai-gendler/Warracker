---
entities:
- entity: warranty
  shows:
  - Product name
  - Purchase date
  - Lifetime
  - Warranty period
  - Expiration date
  - Expiry status
  - Warranty type
  - Vendor
  - Model number
  - Serial numbers
  - Product URL
  - Purchase price
  - Notes
  - Invoice URL
  - Manual URL
  - Files URL
  - Tags
  - Claim summary
  - Currency
  - Archived at
- entity: document
  shows:
  - Kind
  - Storage
- entity: tag
  shows:
  - Name
  - Color
- entity: account
  shows:
  - First name
  - Last name
  - Username
  - Default view
  - Saved filters
  - Expiring soon days
  - Currency symbol
- entity: site-settings
  shows:
  - Global view enabled
  - Global view admin only
entryPoints:
- web: /
- web: /index.html
references:
- kind: code
  role: implementation
  target: frontend/index.html
- kind: code
  role: implementation
  target: frontend/js/controllers/warrantyListController.js
- kind: code
  role: implementation
  target: frontend/js/components/warrantyRenderer.js
---

# Home

The person's warranties: the main list or the archived list, searched, filtered, sorted and shown as a grid, a list or a table, or, in the global scope, everyone's warranties with who added each. Each warranty shows its expiry status, dates, price, serial numbers, tags, claim summary, notes and links to its documents.
