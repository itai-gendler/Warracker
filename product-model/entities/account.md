---
references:
- kind: code
  role: implementation
  target: backend/auth_routes.py
- kind: code
  role: implementation
  target: backend/migrations/003_add_users_table.sql
- kind: code
  role: implementation
  target: backend/migrations/004_create_user_preferences_table.py
- kind: code
  role: implementation
  target: backend/migrations/031_add_owner_role.sql
---

# Account

A person's account on the installation: how they sign in, which role they hold, and the preferences and reminder settings that apply to them whatever their role.

## Information kept

- **Username** — the unique name the person signs in with
- **Email** — the unique address used for signing in, password resets and email reminders
- **First name** — the person's given name, shown as their display name with the last name
- **Last name** — the person's family name
- **Password** — the local password, kept only as verification material; an OIDC SSO account has none
- **Sign-in method** — Local, or OIDC SSO for an account tied to an identity at the single sign-on provider
- **Admin status** — whether the account holds admin rights
- **Application owner** — whether the account is the one Owner of the installation
- **Active status** — whether the account may sign in and receive reminders; deactivated accounts keep their data
- **Last login** — when the person last signed in
- **Preferred language** — the language the interface is shown in, one of the 20 languages Warracker ships
- **Theme** — Light or Dark
- **Default view** — Grid, List or Table, the layout Home opens with
- **Currency symbol** — the symbol prices are displayed with, and the default currency for new warranties
- **Currency position** — whether the symbol appears left or right of amounts
- **Expiring soon days** — how many days before expiry a warranty counts as expiring soon, from 1 to 365, 30 unless changed
- **Date format** — how dates are displayed: month/day/year, day/month/year or year-month-day, in numbers or with the month in words
- **Notification channel** — Disabled, Email, Apprise or Both; Email unless the person chooses otherwise
- **Email notification frequency** — Daily, Weekly (Mondays) or Monthly (the 1st)
- **Email notification time** — the local time of day email reminders go out
- **Email timezone** — the timezone the email notification time is read in
- **Apprise notification time** — the local time of day the person's warranties join Apprise notifications
- **Apprise notification frequency** — the frequency chosen for Apprise notifications
- **Apprise timezone** — the timezone the Apprise notification time is read in
- **View Paperless documents in Warracker** — whether Paperless-ngx documents open inside Warracker instead of in Paperless-ngx; chosen with the Paperless-ngx settings, so only admins set it
- **Saved filters** — the status, tag, vendor, warranty type, search and sort last chosen on Home, restored on the next visit
