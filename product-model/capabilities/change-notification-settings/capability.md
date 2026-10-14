---
availability:
- place: web::signed-in
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py#update_preferences
- kind: code
  role: implementation
  target: frontend/settings-new.html
---

# Change notification settings

A person chooses how they hear about expiring warranties: by email, through Apprise, both or not at all, and for email the frequency, time of day and timezone, and for Apprise the time of day and timezone.
