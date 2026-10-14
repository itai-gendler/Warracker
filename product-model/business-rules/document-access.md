---
appliesTo:
- type: entity
  id: document
  effect: reads
permits:
- related:
  - verb: holds
    entity: warranty
  - verb: owns
    entity: user
- related:
  - verb: holds
    entity: warranty
  - verb: owns
    entity: admin
- related:
  - verb: holds
    entity: warranty
  - verb: owns
    entity: owner
- actors:
  - admin
  - owner
- actors:
  - user
  when:
  - entity: site-settings
    fact: Global view enabled
    is: 'On'
  - entity: site-settings
    fact: Global view admin only
    is: 'Off'
  - fact: Kind
    is-not: Files
references:
- kind: code
  role: implementation
  target: backend/file_routes.py#_check_file_authorization
- kind: code
  role: implementation
  target: backend/file_routes.py#serve_paperless_document
---

# Other people open only a warranty's photo, invoice and manual, through the global view

The person who added a warranty and every admin open any of its documents. Other signed-in people open its product photo, invoice and manual only while the global view is enabled and not limited to admins, and never its other files.
