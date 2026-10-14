---
kind: primary
routes:
  web: Web
steps:
- text: The Visitor enters their email address
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::password-reset
- text: An account has that email
  kind: condition
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts:
    web:
      place: web::public::password-reset
  actor: visitor
- text: The Product emails a reset link valid for 24 hours, replacing any earlier link, and says a link is on its way if the email is registered
  kind: product
  actor: visitor
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Email base URL
  contexts:
    web:
      place: web::public::password-reset
- text: The Visitor follows the link and chooses a new password
  kind: actor
  actor: visitor
  entities: []
  contexts:
    web:
      place: web::public::password-reset
- text: The Product sets the new password, retires the link and opens the sign-in page
  kind: product
  actor: visitor
  entities:
  - entity: account
    effect: changes
    facts:
    - Password
  contexts:
    web:
      place: web::public::password-reset
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#request_password_reset
- kind: code
  role: implementation
  target: backend/auth_routes.py#reset_password
- kind: code
  role: implementation
  target: frontend/reset-password.html
---

# Reset a forgotten password

## Trigger

A Visitor has forgotten the password of their account.

## Outcome

The account has the new password, the link no longer works, and the Visitor is on the sign-in page.

## Edge cases

- The new password must meet the same strength rule as at registration.
