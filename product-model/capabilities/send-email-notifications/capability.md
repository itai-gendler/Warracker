---
domain: admin-actions
availability:
- place: web::signed-in
- place: web::administration
references:
- kind: code
  role: implementation
  target: backend/notifications.py#send_expiration_notifications
- kind: code
  role: implementation
  target: backend/notifications.py#get_expiring_warranties
- kind: code
  role: implementation
  target: backend/notifications.py#is_notification_due
- kind: code
  role: implementation
  target: backend/notifications.py#format_expiration_email
- kind: code
  role: implementation
  target: backend/admin_routes.py#trigger_notifications
---

# Send email notifications

Warracker emails each person whose notification channel is Email or Both a list of their tracked warranties expiring from today through their expiring soon days, at their email notification time in their timezone on the days their frequency includes. An admin can also send the email notifications at once.
