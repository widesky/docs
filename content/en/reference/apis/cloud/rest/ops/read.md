---
title: "Read"
linkTitle: "read"
weight: 6
type: docs
description: >
  Read a set of entity records either by id or by a filter.
---

{{% alert title="Note"  color="primary" %}} Widesky has extends the standard Project-Haystack filter to allow tag value matching by regular expression. The pattern syntax for this feature is currently implemented to the JavaScript's regular expression standard.  Pattern flags like `/i` (case insensitive) are not currently supported.
{{% /alert %}}

## Details

- **URL:** `/api/read`

- **Method:** `POST`

- **Request Data Params (by filter):**  A grid with a single row and following columns:

  |Column|Kind|Value description|
  |------|----|-----------|
  |`filter`|`Str`|Project Haysteck filter to match against desired entities|
  |`limit`|`Number`|Maximum number of matching entities to return in the response|

- **Request Data Params (by id):** A grid with one or more rows with the following columns:

  |Column|Kind|Value description|
  |------|----|-----------|
  |`id`|`Ref`|The UUID or fully qualified name of the entity.|


- **Response (by filter):** A grid with a row for each entity read. If no matches were found this will be an empty grid with no rows.

- **Response: (by id)** A grid with a row for each entity read. Each row corresponds to the request grid and its respective row ordering.

## Examples

### Read by filter

- **Request**
  ```
  POST /api/read HTTP/1.1
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

### Read by id, real-time point
- **Request**
  ```
  POST /api/read HTTP/1.1
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
### Read by fully-qualified name, real-time point
- **Request**
  ```
  POST /api/read HTTP/1.1
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
        "id": "r:site.equip.real-time_point"
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

### Tag value look up by regular expression
- **Request**
  ```
  POST /api/read HTTP/1.1
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
        "filter": "s:area =~ /456178.*/"
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
        "name": "area"
      },
      {
        "name": "dis"
      },
      {
        "name": "space"
      }
    ],
    "rows": [
      {
        "id": "r:92b285bf-5197-44f9-9560-9cc0f7e3f203 A big space",
        "area": "n:456178901",
        "dis": "s:A big space",
        "space": "m:"
      }
    ]
  }
  ```
