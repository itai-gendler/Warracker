---
appliesTo:
- type: entity
  id: warranty
  effect: reads
permits:
- related:
  - verb: owns
    entity: user
- related:
  - verb: owns
    entity: admin
- related:
  - verb: owns
    entity: owner
- actors:
  - user
  when:
  - entity: site-settings
    fact: Global view enabled
    is: 'On'
  - entity: site-settings
    fact: Global view admin only
    is: 'Off'
- actors:
  - admin
  - owner
  when:
  - entity: site-settings
    fact: Global view enabled
    is: 'On'
- unattended: true
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_global_warranties
- kind: code
  role: implementation
  target: backend/statistics_routes.py#get_global_statistics
---

# A warranty is seen by the person who added it and, through the global view, by others

The person who added a warranty always sees it. Other signed-in people see it only while the global view is enabled, and people without admin rights only while it is not limited to admins. Scheduled reminders read the warranties they remind about.
