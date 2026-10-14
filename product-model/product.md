---
id: warracker
summary: 'Self-hosted warranty tracker: purchases with expiry dates, receipts and manuals, warranty claims and expiry alerts by email or Apprise, for individuals and teams with admin controls.'
category: warranty-tracking
tags:
- warranties
- receipts
- self-hosted
- reminders
authors:
- name: sassanix
  url: https://github.com/sassanix
license: AGPL-3.0-only
languages:
- en
- ar
- cs
- de
- es
- fa
- fr
- he
- hi
- it
- ja
- ko
- nl
- pl
- pt
- ru
- tr
- uk
- zh-CN
- zh-HK
limitations:
- 'Warracker is self-hosted: one installation serves the people with accounts on it, and the first account created owns the installation.'
- Every warranty belongs to the one account that added it; there is no shared ownership, and other people see it only through the read-only global view.
- Expiry alerts go out by email or through Apprise to the destinations an admin configures; people do not enter their own Apprise destinations.
- Documents are kept on the Warracker server or, when an admin enables it, in an existing Paperless-ngx instance; Warracker does not read their contents.
- Prices are kept per warranty with their currency but are never converted between currencies.
references:
- kind: doc
  role: intent
  target: README.md
---

# Warracker

Warracker keeps a person's product warranties in one place. Each warranty records the product, when it was bought, how long its coverage lasts (a period from the purchase date, an exact expiration date, or lifetime), what was paid, and its receipt, manual, photo and other files. Warracker works out whether each warranty is active, expiring soon or expired, sends reminders before warranties expire, and tracks the warranty claims made against them through their statuses.

People sign up or sign in with a password or an OIDC single sign-on provider. Each person keeps their own warranties, tags, display preferences and reminder settings. Admins manage the accounts on the installation, the site settings, single sign-on, the Paperless-ngx connection and Apprise notifications, and read an audit trail of their changes; the one Owner can also hand ownership to another admin. When the global view is on, signed-in people can browse everyone's warranties read-only.

## Intent

Warracker exists so that nobody misses warranty coverage they are owed. Its author built it after a family dishwasher broke while the family believed it was still covered, only to find they were looking at the wrong invoice and the warranty had ended months earlier. It brings to warranties the clarity that subscription trackers bring to subscriptions: track purchases, receipts and warranties in one organized place, and be reminded before coverage ends, for individuals and for teams.
