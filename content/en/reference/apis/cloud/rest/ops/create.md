---
title: "Create"
linkTitle: "create"
weight: 5
type: docs
description: >
  Used for adding new entities.
---
{{% alert title="Warning"  color="warning" %}} * The creation of entities must be done methodically to ensure the relationships are formed correctly. To ensure this occurs, create parent entities in a separate request before attempting to create the child entities.
* The create operation is not transactional. That is, if the create operation fails, then those entities which were successfully inserted within the same call will persist in the database and won't be rolled back. This will be addressed in a future release.
* Avoid using the dot '.' in dis tag values. This can interfere with the semantic modeling, causing undesirable behavior.
{{% /alert %}}

---

## Details

**URL:** `/api/createRec`

**Method:** `POST`

**Request Data Params:** *A grid with one or more rows for each entity to be added with the following columns:*

|Column|Required|Value description|
|------|--------|-----------|
|`dis`|✓|A human friendly display name for the entity|
|A primary marker tag for the entity e.g. `site`, `equip`, `space` or `point`|✓|Marker tag indication *m:*|
|`id`| |A user supplied id in place of the WideSky generated UUID|
|*Any other tag e.g. `name`, `elec`, `his`*||*Corresponding tag value*|

**Response:** *A grid with a row for each newly created entity with an additional WideSky generated UUID in the `id` column. The rows in the returned grid will follow the same ordering as those given in the request grid.*

---
## Examples

### Specifying name

**Request:**
  ```json
  POST /api/createRec HTTP/1.1
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
        "dis": "s:My Site",
        "site": "m:",
        "tz": "s:Brisbane"
      }
    ]
  }
  ```
**Response:**
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
        "id": "r:7c7a91bd-d3af-4977-b2c0-65f0dddb6f7b",
        "dis": "s:My Site",
        "site": "m:",
        "tz": "s:Brisbane"
      }
    ]
  }
  ```

### Specifying id

  **Request:**
```json
POST /api/createRec HTTP/1.1
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
      "id": "r:9bd4756a-ff30-4142-ab90-dadb0b8b4b58",
      "dis": "s:My nameless site",
      "site": "m:",
      "tz": "s:Brisbane"
    }
  ]
}
```

  **Response:**
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
      "id": "r:9bd4756a-ff30-4142-ab90-dadb0b8b4b58",
      "dis": "s:My Site",
      "site": "m:",
      "tz": "s:Brisbane"
    }
  ]
}
```
### Specifying name and id

  **Request:**
  ```json
  POST /api/createRec HTTP/1.1
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
        "id": "r:37790aef-44a7-47ce-8dad-623ecde369b7",
        "name": "s:mySiteWithId",
        "dis": "s:My Site, with ID given",
        "site": "m:",
        "tz": "s:Brisbane"
      }
    ]
  }
  ```
  **Response:**
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
      "id": "r:37790aef-44a7-47ce-8dad-623ecde369b7 mySiteWithId",
      "name": "s:mySiteWithId",
      "dis": "s:My Site, with ID given",
      "site": "m:",
      "tz": "s:Brisbane"
    }
  ]
}```