---
domain: apprise-notifications
availability:
- place: web::signed-in
- place: web::administration
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

# Send Apprise notifications

While Apprise is enabled with destinations, Warracker notifies the admin-configured Apprise destinations about warranties reaching each of the notification days before expiry, once per warranty and notification day, at the Apprise notification time of the people whose channel is Apprise or Both. An admin can also send expiration notifications at once.
