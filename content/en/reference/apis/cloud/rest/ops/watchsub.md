---
title: "Watch Subscribe"
linkTitle: "watchSub"
weight: 11
type: docs
description: >
    Create or append `point`s bearing the `cur` tag to a real-time "watch"
    list.
---

## Details

The `watchSub` operation is used for creating watches or adding points to an existing Watch.  [Watches](http://project-haystack.org/doc/Rest#watches) are a mechanism used to provide real-time updates to a Project Haystack client by way of a simple polling-based HTTP API.

Only real-time `point`s (those bearing the `cur` tag) can be used with a watch, any point lacking the `cur` tag will be ignored.

**URL:** `/api/watchSub`

**Method:** `POST`

**Request Data Params (create a watch):** *A grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`watchDis`|`Str`|Display name for the watch|
|`lease`|`Number`|Duration of the lease with unit of time measurement (optional)|

*… and one or more rows with the following columns:*

|Column|Kind|Value Description|
|------|----|-----------|
|`id`|`Ref`|Point to be added to the new watch|

**Request Data Params (append to watch):** *A grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`watchId`|`Str`|The ID of the watch object previously returned by `watchSub`|
|`lease`|`Number`|Duration of the lease with unit of time measurement (optional)|

*… and zero or more rows with the following columns:*

|Column|Kind|Value Description|
|------|----|-----------|
|`id`|`Ref`|Point to be added to the new watch|

**Response (both types):** *A grid with the following metadata fields:*

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

{{% alert title="Note"  color="info" %}}
When appending to an existing watch, the `watchId` returned in the response may differ from that of the request.  The client should update the `watchId` it has stored and use the new `watchId` on subsequent requests.
{{% /alert %}}

---
### Examples:

**Request (create watch):**
```json
POST /api/watchSub HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Bearer <authToken>
Accept: application/json
Content-Type: application/json
  
{
  "meta": {
    "ver": "2.0",
    "lease": "n:1 hr",
    "watchDis": "s:a watch description"
  },
  "cols": [
    {
      "name": "id"
    }
  ],
  "rows": [
    {
      "id": "r:0eb5f7d4-0243-441a-9e29-8695112d9e54"
    },
    {
      "id": "r:665ebbd2-2f4a-4dc6-bcb1-0aff6a9e4032"
    },
    {
      "id": "r:a5f0c453-8125-4507-852f-1643d15efc07"
    }
  ]
}
```

**Request (append to watch):**
```json
POST /api/watchSub HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Bearer <authToken>
Accept: application/json
Content-Type: application/json
  
{
  "meta": {
    "ver": "2.0",
    "watchId": "s:485050d2-4640-45a6-8c81-7ac3eddca2f7"
  },
  "cols": [
    {
      "name": "id"
    }
  ],
  "rows": [
    {
      "id": "r:232a07c8-1aa0-45d2-a0a1-52b59c01b63c"
    }
  ]
}
```

**Response (both request types):**
```json
{
  "meta": {
    "ver": "2.0",
    "lease": "n:1 hr",
    "watchId": "s:63b4bc94-83f5-4813-83ba-59636ef67362"
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
      "curVal": "n:25.4809"
    },
    {
      "id": "r:665ebbd2-2f4a-4dc6-bcb1-0aff6a9e4032 pt2",
      "curStatus": "s:ok",
      "curVal": "n:5.1151"
    },
    {
      "id": "r:a5f0c453-8125-4507-852f-1643d15efc07 pt3",
      "curErr": "Cannot communicate to point.",
      "curStatus": "s:down",
      "curVal": "n:0"
    }
  ]
}
```
