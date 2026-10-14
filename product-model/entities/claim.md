---
domain: warranties
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#create_claim
- kind: code
  role: implementation
  target: backend/migrations/044_create_warranty_claims_table.sql
- kind: code
  role: implementation
  target: frontend/js/components/claims.js
---

# Claim

A warranty claim made against one warranty, tracked from filing to its outcome.

## Information kept

- **Claim date** — when the claim was made; required
- **Claim number** — the reference the seller or manufacturer gave the claim
- **Description** — what the claim is about
- **Resolution** — how the claim was resolved
- **Resolution date** — when it was resolved

## States

### Submitted

The claim has been filed and awaits an answer.

### In Progress

The claim is being handled.

### Approved

The claim was accepted.

### Denied

The claim was refused.

### Resolved

The claim is settled.

### Cancelled

The claim was withdrawn.
