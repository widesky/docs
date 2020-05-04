---
title: "History Write"
linkTitle: "hisWrite"
weight: 10
type: docs
description: >
    Store historical data in a point
---

The hisWrite operation is used to write time series data to one or more historised points. You can perform a write on a single point, or write to multiple points using our extended multi-point feature. The hisWrite operation also supports time zone conversion including daylight savings.

## Details

- **URL:** `/api/hisWrite`
- **Method:** `POST`
- **Request Data Params (single point):** A grid with the following metadata fields:

  |Column|Required|Kind|Value description|
  |------|--------|----|-----------------|
  |`id`|✓|`Ref`|ID of the point we intend to write|

  and one or more rows with the following columns:

  |Column|Required|Kind|Value description|
  |------|--------|----|-----------------|
  |`ts`|✓|`DateTime`|A dateTime formatted sample time-stamp e.g. `2000-03-26T02:01:00+10:00 Sydney`|
  |`val`|✓|See `point`'s `kind` tag|Value to be recorded for the point at that time|

- **Request Data Params (multiple points):** A grid with zero or more rows and the following columns:

  |Column|Required|Kind|Value description|
  |------|--------|----|-----------------|
  |`ts`|✓|`DateTime`|A dateTime formatted sample time-stamp e.g. `2000-03-26T02:01:00+10:00 Sydney`|
  |`v0`|✓|See `kind` of `point` referenced by column's `id` field|The first `point` to write history records to.  Column Metadata should have `Ref` field `id` referencing the `point` to write.|
  |`v1`||See `kind` of `point` referenced by column's `id` field|The second `point` to write history records to.  Column Metadata should have `Ref` field `id` referencing the `point` to write.|
  |…||…|… etc …|
  |`vN`||See `kind` of `point` referenced by column's `id` field|The nth `point` to write history records to.  Column Metadata should have `Ref` field `id` referencing the `point` to write.|

- **Response (both types):** *Empty Grid.*
  The returned grid will have no rows or columns -- the `err` field should be checked in the grid's metadata in case of errors.

{{% alert title="Tip"  color="primary" %}}
-   The value kind of the posted data must match the entity's configured kind.
- For futher details on how time-stamps are formatted, see the Project Haystack documentation for the [ZINC](https://www.project-haystack.org/doc/Zinc#literals) or [JSON](https://www.project-haystack.org/doc/Json#mapping) grid formats.
{{% /alert %}}


## Time zones

The `hisWrite` operation supports automatic time zone conversion.  When you perform a `hisWrite` request with a time zone range specifying one or more `DateTime` values, the resulting data set retrieved will be automatically converted to the time zone matching the one given in the `range` field.

### Daylight Savings

In cases where the time zone is influenced by Daylight Savings Time, the UTC offset given in the `DateTime` values (`ts` column) will be advanced by 1 hour ahead of the nominal UTC offset for that region. Days that transition to or form daylight savings are also supported.


## Examples:

### Single point

- **Request:**
  ```
  POST /api/hisWrite HTTP/1.1
  Host: example.on.widesky.cloud
  Authorization: Bearer <authToken>
  Accept: application/json
  Content-Type: application/json

  {
    "meta": {
      "ver": "2.0",
      "id": "r:5cdf0de0-a687-4fff-a74a-e710dc9218eb"
    },
    "cols": [
      {
        "name": "ts"
      },
      {
        "name": "val"
      }
    ],
    "rows": [
      {
        "ts": "t:2016-01-01T00:00:00-00:00 UTC",
        "val": "n:1"
      },
      {
        "ts": "t:2016-01-01T01:00:00-00:00 UTC",
        "val": "n:2"
      }
    ]
  }
  ```
- **Response:**
  ```
  {
    "meta": {
      "ver": "2.0"
    },
    "cols": [
      {
        "name": "empty"
      }
    ],
    "rows": []
  }
  ```

### Multiple points
**Request:**
  ```
  POST /api/hisWrite HTTP/1.1
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
        "name": "ts"
      },
      {
        "name": "v0",
        "id": "r:5cdf0de0-a687-4fff-a74a-e710dc9218eb"
      },
      {
        "name": "v1",
        "id": "r:d83e6530-e802-494f-aae8-8da6395902db"
      }
    ],
    "rows": [
      {
        "ts": "t:2016-01-01T00:00:00-00:00 UTC",
        "v0": "n:1.0",
        "v1": "n:2.0"
      },
      {
        "ts": "t:2016-01-01T01:00:00-00:00 UTC",
        "v0": "n:3.0",
        "v1": "n:4.0"
      }
    ]
  }
  ```

- **Response:**
  ```
  {
    "meta": {
      "ver": "2.0"
    },
    "cols": [
      {
        "name": "empty"
      }
    ],
    "rows": []
  }
  ```
