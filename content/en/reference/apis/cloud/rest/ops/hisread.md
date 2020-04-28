---
title: "History Read"
linkTitle: "hisRead"
weight: 9
type: docs
description: >
    Retrieve historical data from a `point` entity bearing the `his` tag.
---

The hisRead operation is used to read time-series data from one or more historised points. You can perform a query on a single point, or read from multiple points using our extended multi-point query.


{{% alert title="Tip"  color="primary" %}}
For more advanced mathematical operations used for data analysis, use the GraphQL [History](../../../graphql/schema/#history) Object
{{% /alert %}}


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

|`range` value|Time range selected|
|-------------|-------------------|
|`first`|The oldest (least recent) sample|
|`last`|The newest (most recent) sample|
|`today`|All of the samples from midnight of the current day to midnight tomorrow|
|`yesterday`|All of the samples from midnight of the previous day to midnight of the current day|
|`{DT}`|All of the samples at and following the timestamp given by `{DT}`|
|`{DT},{DT}`|All of the samples between the two timestamps starting at and including the start `{DT}` and finishing *before* (and excluding) the end `{DT}`|
|`{D}`|All of the samples from midnight of the date defined to midnight of the day following the defined date|
|`{D},{D}`|All of the samples that fall on or after the first `{D}` and on or before the second `{D}`|

… where:

* `{D}` is a `Date` value (e.g. `2015-07-24`)
* `{DT}` is a `DateTime` (e.g. `2015-07-24T10:34:15+10:00 Brisbane`)

For futher details on how these are formatted, see the Project Haystack documentation for the [ZINC](https://www.project-haystack.org/doc/Zinc#literals) or [JSON](https://www.project-haystack.org/doc/Json#mapping) grid formats.

When specifying `DateTime` ranges (that is, ranges of the form `${DT},${DT}`), the time range selected is **inclusive** of the start `DateTime` value and **exclusive** of the end `DateTime` value.  When the range uses `Date`s instead, the value is inclusive of *both* date values given.  For example:

|Range Template|Literal Example|Effective range|
|--------------|---------------|---------------|
|`{DT}`|`2020-04-27T10:00+10:00 Brisbane`|Any sample taken exactly at or after 10:00AM AEST on the 27th April|
|`{DT},{DT}`|`2020-04-27T08:30+10:00 Brisbane,2020-04-27T17:00+10:00 Brisbane`|All samples taken between 8:30AM and 5:00PM on the 27th April **including** exactly 8:30:00.000 AM right up to 4:59:59.999 PM but **excluding** 5:00:00.000 PM.|
|`{D}`|`2020-04-27`|All samples taken immediately at midnight or after AEST on the 27th, right up to 11:59:59.999 PM that same day, **excluding** exactly midnight AEST on the 28th.|
|`{D},{D}`|`2020-04-27,2020-05-01`|All samples taken immediately at midnight or after AEST on the 27th, right up to 11:59:59.999 PM on the 1st, **excluding** exactly midnight AEST on the 2nd.|

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

**Response (multiple point):** *Grid with the following metadata fields:*

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

### Time-zone conversion

The `hisRead` operation supports automatic time-zone conversion.  When you perform a `hisRead` request with a time-zone range specifying one or more `DateTime` values, the resulting data set retrieved will be automatically converted to the time-zone matching the one given in the `range` field.

#### Daylight Savings Time support

In cases where the time-zone is influenced by Daylight Savings Time, the UTC offset given in the `DateTime` values (`ts` column) will be advanced by 1 hour ahead of the nominal UTC offset for that region:

```json
{
  "meta": {
    "ver": "2.0",
    "hisEnd": "t:2000-03-26T02:01:00+10:00 Sydney",
    "hisStart": "t:2000-03-26T02:00:00+11:00 Sydney",
    "id": "r:13641c0a-8e88-41b5-b3ed-75240d8b9bb2"
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
      /* DST active */
      "ts": "t:2000-03-26T02:00:00+11:00 Sydney",
      "val": "n:120 kWh"
    },
    {
      /* DST inactive */
      "ts": "t:2000-03-26T02:00:00+10:00 Sydney",
      "val": "n:150 kWh"
    }
  ]
}
```

#### Requests *without* time-zones given

If your `range` parameter does not specify a `DateTime` value explicitly (e.g. `today`', `yesterday`, `first`, `last`, or a range involving plain `Date`s), then the time-zone information is taken from the points in the request.  In the case where all points exist in the same time-zone, the records returned will all be returned *in that same time-zone*.

If one or more points however has a *different* time-zone, the [`Rel` time-zone](https://fantom.org/doc/sys/TimeZone#rel) is used.  This time-zone has a 0-minute offset from UTC, and is used to indicate that all data in the response has been *normalised* to this common time-zone.  For example:

```json
{
  "meta": {
    "ver": "2.0",
    "hisEnd": "t:2016-01-01T00:00:00-00:00 Rel",
    "hisStart": "t:2016-01-01T00:00:00-00:00 Rel"
  },
  "cols": [
    {
      "name": "ts"
    },
    {
      "name": "v0",
      "id": "r:00000111-0000-0000-0000-000000000000"
    },
    {
      "name": "v1",
      "id": "r:00000112-0000-0000-0000-000000000000"
    }
  ],
  "rows": [
    {
      "ts": "t:2016-01-01T00:00:00-00:00 Rel",
      "v0": "n:1 Wh",
      "v1": "n:1 Wh"
    }
  ]
}
```

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
