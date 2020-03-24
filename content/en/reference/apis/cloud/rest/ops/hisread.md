---
title: "History Read"
linkTitle: "hisRead"
weight: 9
type: docs
description: >
    Retrieve historical data from a `point` entity bearing the `his` tag.
---

## Details

**URL:** `/api/hisRead`

**Method:** `POST`

**Request Data Params (single point):** *A grid with a single row and the following columns:*

|Column|Kind|Value description|
|------|----|-----------|
|`id`|`Ref`|The `point` to read history records from.|
|`range`|`Str`|The time range to retrieve from time-series storage.|

**Request Data Params (multiple points):** *A grid with a single row and the following columns:*

|Column|Kind|Value description|
|------|----|-----------|
|`range`|`Str`|The time range to retrieve from time-series storage.|
|`id0`|`Ref`|The first `point` to read history records from.|
|`id1`|`Ref`|The second `point` to read history records from.|
|…|…|… etc …|
|`idN`|`Ref`|The _n_th `point` to read history records from.|

**Range values (both request types):**

The `range` parameter (common to both request types) is a string
with one of the following formats:

|`range`|Time range selected|
|-------|-------------------|
|`first`|The oldest (least recent) sample|
|`last`|The newest (most recent) sample|
|`today`|All of the samples from midnight of the current day to midnight tomorrow
|`yesterday`|All of the samples from midnight of the previous day to midnight of the current day|
|`{DT}`|All of the samples after a given timestamp|
|`{DT},{DT}`|All of the samples between the two timestamps|
|`{D}`|All of the samples from midnight of the date defined to midnight of the day following the defined date|
|`{D},{D}`|All of the samples from midnight of the first date defined to midnight of the day following the second date defined|

… where `{D}` is a `Date` value (e.g. `2015-07-24`) and `{DT}` is a `DateTime` (e.g. `2015-07-24T10:34:15+1000 Brisbane`).

**Response (single point):** *Grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`id`|`Ref`|ID of the point we just read|
|`hisStart`|`DateTime`|Timestamp for range start in `point`'s timezone|
|`hisEnd`|`DateTime`|Timestamp for range end in `point`'s timezone|

*then zero or more rows with the following columns:*

|Column|Kind|Value Description|
|------|----|-----------|
|`ts`|`DateTime`|Sample time-stamp|
|`val`|See `point`'s `kind` tag|Value recorded for the point at that time|

**Response (single point):** *Grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`hisStart`|`DateTime`|Timestamp for range start in `point`'s timezone|
|`hisEnd`|`DateTime`|Timestamp for range end in `point`'s timezone|

*then zero or more rows with the following columns:*

|Column|Kind|Value Description|
|------|----|-----------|
|`ts`|`DateTime`|Sample time-stamp|
|`v0`|See `kind` tag of `id0`|Value recorded for `id0` at that time|
|`v1`|See `kind` tag of `id1`|Value recorded for `id1` at that time|
|…|…|… etc …|
|`vN`|See `kind` tag of `idN`|Value recorded for `idN` at that time|

---
### Examples:

**Request (single point):**
```json
POST /api/hisRead HTTP/1.1
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
    },
    {
      "name": "range"
    }
  ],
  "rows": [
    {
      "id": "r:5cdf0de0-a687-4fff-a74a-e710dc9218eb",
      "range": "s:2016-01-01"
    }
  ]
}
```
**Response (single point):**
```json
{
  "meta": {
    "ver": "2.0",
    "hisEnd": "t:2016-01-02T00:00:00Z UTC",
    "hisStart": "t:2016-01-01T00:00:00Z UTC",
    "id": "r:5cdf0de0-a687-4fff-a74a-e710dc9218eb myPoint"
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
      "ts": "t:2016-01-01T01:00:00Z UTC",
      "val": "n:2"
    }
  ]
}
```

**Request (multiple points):**
```json
POST /api/hisRead HTTP/1.1
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
      "name": "range"
    },
    {
      "name": "id0"
    },
    {
      "name": "id1"
    }
  ],
  "rows": [
    {
      "id0": "r:5cdf0de0-a687-4fff-a74a-e710dc9218eb",
      "id1": "r:d83e6530-e802-494f-aae8-8da6395902db",
      "range": "s:2016-01-01"
    }
  ]
}
```
**Response (multiple points):**
```json
{
  "meta": {
    "ver": "2.0",
    "hisEnd": "m:",
    "hisStart": "m:"
  },
  "cols": [
    {
      "name": "ts"
    },
    {
      "id": "r:5cdf0de0-a687-4fff-a74a-e710dc9218eb myPoint",
      "name": "v0"
    },
    {
      "id": "r:d83e6530-e802-494f-aae8-8da6395902db myPoint1",
      "name": "v1"
    }
  ],
  "rows": [
    {
      "ts": "t:2016-01-01T00:00:00Z UTC",
      "v0": "n:1",
      "v1": "n:1"
    }
  ]
}
```
