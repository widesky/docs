---
title: "Delete"
linkTitle: "delete"
weight: 8
type: docs
description: >
  Delete one or more entities matched by ID or matching a filter expression.
---

Entities can be removed either by specifying an id or by using a filter. Entities can only be removed if they don't have child references to avoid orphaned entities.


{{% alert title="Note"  color="primary" %}}
The delete operation is not transactional. That is, if the delete operation fails, then those entities which were successfully deleted within the same call will be removed from the the database and won't be rolled back. This will be addressed in a future release.
{{% /alert %}}



## Details

- **URL:** `/api/deleteRec`

- **Method:** `POST`

- **Request Data Params (by filter):** A grid with a single row and following columns:

  |Column|Kind|Value description|
  |------|----|-----------|
  |`filter`|`Str`|Project Haysteck filter to match against desired entities|
  |`limit`|`Number`|Maximum number of matching entities to return in the response|

- **Request Data Params (by id):** A grid with one or more rows with the following columns:

  |Column|Kind|Value description|
  |------|----|-----------|
  |`id`|`Ref`|The UUID or fully qualified name of the entity.|

- **Response (by filter):** A grid with a row for each entity deleted. If no matches were found this will be an empty grid with no rows.

- **Response: (by id)** A grid with a row for each entity deleted. Each row corresponds to the request grid and its respective row ordering.

## Examples

### Delete by filter

- **Request**
  ```
  POST /api/deleteRec HTTP/1.1
  Host: example.on.widesky.cloud
  Authorization: Bearer <authToken>
  Accept: application/json
  Content-Type: application/json

  {
    "meta": {
      "ver": "2.0"
    },
    "cols": [
      {
        "name": "filter"
      }
    ],
    "rows": [
      {
        "filter": "s:site"
      }
    ]
  }
  ```
- **Response**
  ```
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
        "id": "r:192c29f7-c314-4cf6-a1e6-6361f6f666eb site",
        "name": "s:site",
        "dis": "s:Site description",
        "site": "m:",
        "tz": "s:Brisbane"
      }
    ]
  }
  ```


### Delete by id
- **Request**
  ```
  POST /api/deleteRec HTTP/1.1
  Host: example.on.widesky.cloud
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
      }
    ],
    "rows": [
      {
        "id": "r:1ccbe79f-6c81-449b-b263-df59b04e9889"
      }
    ]
  }
  ```
- **Response**
  ```
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
        "name": "cur"
      },
      {
        "name": "curErr"
      },
      {
        "name": "curStatus"
      },
      {
        "name": "curVal"
      },
      {
        "name": "dis"
      },
      {
        "name": "equipRef"
      },
      {
        "name": "kind"
      },
      {
        "name": "point"
      },
      {
        "name": "sensor"
      },
      {
        "name": "siteRef"
      },
      {
        "name": "tz"
      }
    ],
    "rows": [
      {
        "id": "r:1ccbe79f-6c81-449b-b263-df59b04e9889 real-time_point",
        "name": "s:real-time_point",
        "dis": "s:Sample real-time point",
        "cur": "m:",
        "curStatus": "s:ok",
        "curVal": "n:500",
        "equipRef": "r:e09d66a2-0d5b-47a7-b4d8-617447146e2f equip",
        "kind": "s:Number",
        "point": "m:",
        "sensor": "m:",
        "siteRef": "r:192c29f7-c314-4cf6-a1e6-6361f6f666eb site",
        "tz": "s:Brisbane"
      }
    ]
  }
  ```
