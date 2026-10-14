---
kind: primary
routes:
  web: Web
steps:
- text: The Owner selects another active admin and confirms the transfer
  kind: actor
  actor: owner
  entities:
  - entity: account
    as: new-owner-account
    effect: reads
    facts:
    - Username
    - Admin status
    - Active status
  - entity: admin
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::ownership-management
- text: The Product makes the chosen account the application owner and the previous one a regular admin
  kind: product
  actor: owner
  entities:
  - entity: account
    as: previous-owner-account
    effect: changes
    facts:
    - Application owner
  - entity: account
    as: new-owner-account
    effect: changes
    facts:
    - Application owner
  - entity: admin
    effect: reads
    facts: []
  contexts:
    web:
      place: web::administration::ownership-management
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#transfer_ownership
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Transfer ownership

## Trigger

The Owner wants another admin to own the installation.

## Outcome

The chosen admin is the Owner; the previous Owner is a regular admin and no longer sees ownership management.
