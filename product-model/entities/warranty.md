---
domain: warranties
relations:
- entity: document
  verb: holds
  cardinality: one-to-many
- entity: claim
  verb: has
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py
- kind: code
  role: implementation
  target: backend/migrations/000_create_warranties_table.sql
- kind: code
  role: implementation
  target: backend/migrations/021_change_warranty_duration_to_components.sql
- kind: code
  role: implementation
  target: backend/migrations/045_add_archived_at_to_warranties.sql
- kind: code
  role: implementation
  target: frontend/js/lib/warrantyProcessing.js
---

# Warranty

The warranty coverage of one purchased product, kept by the person who added it.

## Information kept

- **Product name** — what was bought; required, at most 255 characters
- **Purchase date** — when it was bought; required
- **Lifetime** — whether the coverage never expires
- **Warranty period** — the years, months and days of coverage counted from the purchase date
- **Expiration date** — the last day of coverage, from the purchase date and warranty period or entered exactly; none for a lifetime warranty
- **Expiry status** — Expired, Expiring soon, Active or Lifetime, worked out from the expiration date and the viewer's expiring soon days
- **Warranty type** — Standard, Extended, Manufacturer, Third Party, Store, Premium, Limited, Full, Parts Only, Labor Only, International, Accidental Damage, or a custom type
- **Vendor** — the seller it was bought from
- **Model number** — the product's model number
- **Serial numbers** — any number of serial numbers for the product
- **Product URL** — a link to the product page
- **Purchase price** — what was paid; never negative
- **Currency** — the currency of the purchase price, defaulting to the currency of the person's currency symbol
- **Notes** — free-text notes
- **Invoice URL** — a link to the invoice kept elsewhere
- **Manual URL** — a link to the manual kept elsewhere
- **Files URL** — a link to other files kept elsewhere
- **Tags** — the tags of the person who added it attached to this warranty
- **Claim summary** — No claims, Open while any claim is Submitted or In Progress, otherwise Finished
- **Archived at** — when the warranty was archived

## States

### Tracked

The warranty is on the main list, counts in the status dashboard and gets expiry reminders.

### Archived

The warranty is set aside on the archived list: it keeps everything it holds, but leaves the main list, the dashboard counts other than Archived, and scheduled reminders.
