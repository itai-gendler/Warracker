---
kind: primary
routes:
  web: Web
steps:
- text: The User confirms deleting their account in the danger zone
  kind: actor
  actor: user
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::signed-in::settings
- text: The Product deletes the account with all its warranties, tracked or archived, and everything else it keeps
  kind: product
  actor: user
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
      place: web::signed-in::settings
- text: The Product signs the person out
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::settings
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#delete_account
- kind: code
  role: implementation
  target: frontend/settings-new.js
---

# Delete own account

## Trigger

A User no longer wants their account.

## Outcome

The account, its warranties with their documents and claims, and its tags are gone, and the person is signed out.
