---
kind: primary
routes:
  web: Web
steps:
- text: The Admin chooses Delete for another account and confirms
  kind: actor
  actor: admin
  entities:
  - entity: account
    effect: reads
    facts:
    - Username
  contexts:
    web:
      place: web::administration::users
- text: The Product deletes the account with all its warranties, tracked or archived, and everything else it keeps
  kind: product
  actor: admin
  entities:
  - entity: account
    effect: removes
  - entity: warranty
    as: tracked-warranty
    effect: removes
    from: Tracked
  - entity: warranty
    as: archived-warranty
    effect: removes
    from: Archived
  contexts:
    web:
      place: web::administration::users
references:
- kind: code
  role: implementation
  target: backend/admin_routes.py#delete_user
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Delete a person's account

## Trigger

An Admin removes someone who no longer uses the installation.

## Outcome

The account, its warranties with everything they hold, and its tags are gone, and the deletion is in the audit trail.
