---
kind: primary
routes:
  web: Web
steps:
- text: It is the Apprise notification time of an active person whose channel is Apprise or Both, and Apprise is enabled with destinations
  kind: condition
  unattended: true
  entities:
  - entity: account
    effect: reads
    facts:
    - Active status
    - Notification channel
    - Apprise notification time
    - Apprise timezone
  - entity: site-settings
    effect: reads
    facts:
    - Apprise enabled
    - Apprise URLs
  contexts:
    web:
      place: web::signed-in
- text: The Product picks the person's tracked warranties that have reached a notification day not yet notified for them
  kind: product
  entities:
  - entity: warranty
    effect: reads
    facts:
    - Product name
    - Expiration date
    - Lifetime
  - entity: site-settings
    effect: reads
    facts:
    - Notification days
    - Warranty scope
  contexts:
    web:
      place: web::signed-in
- text: The Product sends the notifications to the Apprise destinations, grouped by days left, and marks those notification days as notified
  kind: product
  entities:
  - entity: site-settings
    effect: reads
    facts:
    - Apprise notification mode
    - Message title prefix
    - Apprise URLs
  contexts:
    web:
      place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/notifications.py#process_apprise_notifications
- kind: code
  role: implementation
  target: backend/notifications.py#filter_to_due_thresholds
- kind: code
  role: implementation
  target: backend/apprise_handler.py
- kind: code
  role: implementation
  target: backend/admin_routes.py#trigger_apprise_expiration_notifications
- kind: code
  role: implementation
  target: backend/migrations/051_add_notification_log.sql
---

# Send scheduled Apprise notifications

## Trigger

It is the Apprise notification time, in their timezone, of a person whose channel is Apprise or Both, and Apprise is enabled with destinations.

## Outcome

The Apprise destinations receive a notification per number of days left, listing up to ten warranties each; every included warranty is not notified again for that notification day.

## Decision points

### Notification mode

Which Apprise notification mode is set?

- Global Summary → one notification per number of days left covers every person due at this time.
- Per User → each person's due warranties are sent as their own notifications.

### Warranty scope

Which warranty scope is set?

- All Users' Warranties → every due person's warranties are included.
- Admin's Warranties Only → only the warranties of the Owner, or of the first admin when there is no Owner, are included.

## Edge cases

- A warranty that passes a notification day while no run happens is notified at the next run, once.
- A notification day is marked notified only when its notification was sent.
