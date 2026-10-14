---
kind: validation
routes:
  web: Web
steps:
- text: The User attaches an invoice, manual or file that is not a PDF, PNG, JPG, JPEG, WEBP, GIF, ZIP or RAR, or a photo that is not an image, and submits
  kind: actor
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::add-warranty
- text: The Product reports that the file type is not allowed
  kind: product
  actor: user
  entities: []
  contexts:
    web:
      place: web::signed-in::add-warranty
references:
- kind: code
  role: implementation
  target: backend/warranties_routes.py#add_warranty
- kind: code
  role: implementation
  target: frontend/js/components/addWarrantyForm.js
- kind: code
  role: implementation
  target: backend/utils.py#allowed_file
---

# Add a warranty with a file of the wrong type

## Trigger

A User attaches a file type Warracker does not keep.

## Outcome

The Product refuses the file type and nothing is added.

## Edge cases

- An upload larger than the installation's upload limit, 32 MB unless the deployment sets another, is refused as too large.
