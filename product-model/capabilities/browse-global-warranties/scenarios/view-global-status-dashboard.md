---
kind: primary
routes:
  web: Web
steps:
- text: The User chooses the global scope on the status dashboard
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::status-dashboard
- text: The global view is enabled and not restricted to administrators
  kind: condition
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Global view enabled
    - Global view admin only
  contexts:
    web:
      place: web::signed-in::status-dashboard
  actor: user
- text: The Product shows the counts, charts and table for every warranty with the name of the person who added it
  kind: product
  actor: user
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Expiration date
    - Expiry status
    - Purchase price
  - entity: account
    effect: reads
    facts:
    - First name
    - Last name
    - Username
  contexts:
    web:
      place: web::signed-in::status-dashboard
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_global_warranties
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_global_warranties_archived
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_global_statistics
- kind: code
  role: implementation
  target: frontend/js/components/warrantyRenderer.js
---

# View the global status dashboard

## Trigger

A User switches the status dashboard to the global scope.

## Outcome

The dashboard counts, charts and table cover everyone's warranties, the table showing who added each.
