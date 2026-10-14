---
appliesTo:
- type: entity
  id: claim
  effect: reads
permits:
- related:
  - verb: has
    entity: warranty
  - verb: owns
    entity: user
- related:
  - verb: has
    entity: warranty
  - verb: owns
    entity: admin
- related:
  - verb: has
    entity: warranty
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
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#get_claims
---

# A warranty's claims are seen by the person who added it and, through the global view, by others

Claims are read by the person who added the warranty, and by other people only through the global view on the same terms as the warranty itself; admins have no other way to read them.
