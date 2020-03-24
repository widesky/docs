---
title: "Update"
linkTitle: "update"
weight: 7
type: docs
description: >
  Modifying existing entity records. It allows you to add new tags, remove existing tags, and modify tag values.
---

{{% alert title="Warning"  color="warning" %}} The create operation is not transactional. That is, if the create operation fails, then those entities which were successfully inserted within the same call will persist in the database and won't be rolled back. This will be addressed in a future release.
{{% /alert %}}



## Details

**URL:** `/api/updateRec`

**Method:** `POST`

**Request Data Params:** *A grid of records containing all entity records to be updated on the server.*

{{% alert title="Note"  color="primary" %}} * To remove existing tags, set the tag value to `x:` (JSON) or `R` (ZINC).
* Prior to performing an Update, the client should do a Read to ensure it has the latest version of the entity to be modified.
* It is not possible to update the identifier tag (`id`) value or the primary tag of an entity
{{% /alert %}}

**Response:** *A grid with a row for each entity updated. Each row corresponds to the request grid and its respective row ordering.*


---

## Examples

### Change Entity description

**Request**
```json
POST /api/updateRec HTTP/1.1
Host: example.com
Authorization: Bearer <authToken>
Accept: application/json
Content-Type: application/json

{
  "meta": {
    "ver": "2.0"
  },
  "cols": [
    {
      "name": "id"
    },
    {
      "name": "dis"
    }
  ],
  "rows": [
    {
      "id": "r:16978738-34be-42f9-8195-fa9f450e18bf",
      "dis": "s:My new site description"
    }
  ]
}
```
**Response**
```json
{
  "meta": {
    "ver": "2.0"
  },
  "cols": [
    {
      "name": "id"
    },
    {
      "name": "name"
    },
    {
      "name": "dis"
    },
    {
      "name": "site"
    },
    {
      "name": "tz"
    }
  ],
  "rows": [
    {
      "id": "r:16978738-34be-42f9-8195-fa9f450e18bf mySite",
      "name": "s:mySite",
      "dis": "s:My new site description",
      "site": "m:",
      "tz": "s:Brisbane"
    }
  ]
}
```
