---
title: "Watch Poll"
linkTitle: "watchPoll"
weight: 12
type: docs
description: >
    Fetch the current values of all `point`s listed on an existing watch list.
---

## Details

The `watchPoll` operation is used to enquire a [watch](http://project-haystack.org/doc/Rest#watches) for real-time updates on the subscribed points. Unless the `refresh` marker is specified in the metadata, only points that have changed since the last poll are returned.

**URL:** `/api/watchPoll`

**Method:** `POST`

**Request Data Params:** *A grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`watchId`|`Str`|The ID of the watch object previously returned by `watchSub`|
|`refresh`|`Marker`|If present, requests the server returns the values of *all* points on the watch list, not just those which have changed.|

*The grid body is not critical.*

**Response:** *A grid with the following metadata fields:*


|Field|Kind|Value Description|
|------|----|-----------|
|`watchId`|`Str`|The ID of the watch object created or updated by `watchSub`|
|`lease`|`Number`|Duration of the lease with unit of time measurement (optional)|

*…and one or more rows with the following columns:*

|Column|Kind|Value Description|
|------|----|-----------|
|`id`|`Ref`|ID of a point in the watch list|
|`curErr`|`Str`|(Optional) Error message detail for non-"OK" states, see [`curErr`](https://www.project-haystack.org/tag/curErr)|
|`curStatus`|`Str`|Status of the point being watched, see [`curStatus`](https://www.project-haystack.org/tag/curStatus)|
|`curVal`|See `kind` tag of `point`|Value last read from the point, if known|

---
### Examples:

**Request (changed points only):**
```json
POST /api/watchPoll HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Bearer <authToken>
Accept: application/json
Content-Type: application/json
 
{
  "meta": {
    "ver": "2.0",
    "watchId": "s:365e89d0-d16b-11e6-bd2a-91507bf01422"
  },
  "cols": [
    {
      "name": "id"
    }
  ],
  "rows": []
}
```

**Request (fetch all points):**
```json
POST /api/watchPoll HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Bearer <authToken>
Accept: application/json
Content-Type: application/json
  
{
  "meta": {
    "ver": "2.0",
    "refresh": "m:",
    "watchId": "s:48ebed40-d3c8-11e6-bcea-f7689c06a4e5"
  },
  "cols": [
    {
      "name": "id"
    }
  ],
  "rows": []
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
      "name": "id"
    },
    {
      "name": "curErr"
    },
    {
      "name": "curVal"
    },
    {
      "name": "curStatus"
    }
  ],
  "rows": [
    {
      "id": "r:0eb5f7d4-0243-441a-9e29-8695112d9e54 pt1",
      "curStatus": "s:ok",
      "curVal": "n:128.6915"
    },
    {
      "id": "r:665ebbd2-2f4a-4dc6-bcb1-0aff6a9e4032 pt2",
      "curStatus": "s:ok",
      "curVal": "n:99.1500"
    },
    {
      "id": "r:a5f0c453-8125-4507-852f-1643d15efc07 pt3",
      "curStatus": "s:ok",
      "curVal": "n:83.7754"
    }
  ]
}
```
