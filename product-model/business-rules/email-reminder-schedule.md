---
appliesTo:
- type: capability
  id: send-email-notifications
- type: entity
  id: account
  facts:
  - Email notification frequency
  - Email notification time
  - Email timezone
  - Expiring soon days
references:
- kind: code
  role: implementation
  target: backend/notifications.py#send_expiration_notifications
---

# Email reminders list every warranty expiring within the person's expiring soon days

At their email notification time, in their timezone, on every day, every Monday or the 1st of each month as their frequency says, an active person whose notification channel is Email or Both is emailed every tracked warranty of theirs that is not lifetime and expires from today through their expiring soon days. No email is sent when none is due.
