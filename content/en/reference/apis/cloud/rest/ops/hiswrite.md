---
title: "History Write"
linkTitle: "hisWrite"
weight: 10
type: docs
description: >
    Store historical data in a `point` entity bearing the `his` tag.
---

## Timezone conversion


## Details

**URL:** `/api/hisWrite`

**Method:** `POST`

**Request Data Params (single point):** *A grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`id`|`Ref`|ID of the point we intend to write|

*… and one or more rows with the following columns:*

|Column|Kind|Value Description|
|------|----|-----------|
|`ts`|`DateTime`|Sample time-stamp|
|`val`|See `point`'s `kind` tag|Value to be recorded for the point at that time|

**Request Data Params (multiple points):** *A grid with zero or more rows and the following columns:*

|Column|Kind|Value description|
|------|----|-----------|
|`ts`|`DateTime`|Sample time-stamp|
|`v0`|See `kind` of `point` referenced by column's `id` field|The first `point` to write history records to.  Column Metadata should have `Ref` field `id` referencing the `point` to write.|
|`v1`|See `kind` of `point` referenced by column's `id` field|The second `point` to write history records to.  Column Metadata should have `Ref` field `id` referencing the `point` to write.|
|…|…|… etc …|
|`vN`|See `kind` of `point` referenced by column's `id` field|The _n_th `point` to write history records to.  Column Metadata should have `Ref` field `id` referencing the `point` to write.|

**Response (both types):** *Empty Grid.*  The returned grid will have no rows or columns -- the `err` field should be checked in the grid's metadata in case of errors.

---
### Examples:

**Request (single point):**
```json
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

**Request (multiple points):**
```json
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

**Response (both request types):**
```json
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
