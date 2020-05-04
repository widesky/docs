---
title: "Watch Poll"
linkTitle: "watchPoll"
weight: 12
type: docs
description: >
    Fetch the current values of all `point`s listed on an existing watch list.
---

The `watchPoll` operation is used for real-time updated on subscribed points after obtaining a watchId from the [`watchSub`](../watchsub) op. Unless the `refresh` marker is specified in the metadata, only points that have changed since the last poll are returned.


{{% alert title="Tip"  color="primary" %}}
Instead of a client routinly using watchPoll to obtain new data, you can instead use the [websockets](../../websocket) extension to recieve real-time update notifications after obtaining a watchId.
{{% /alert %}}

## Details

- **URL:** `/api/watchPoll`

- **Method:** `POST`

- **Request Data Params:** A grid with the following metadata fields:

  |Meta Field|Required|Kind|Value Description|
  |------|----|-|-----------|
  |`watchId`|✓|`Str`|The ID of the watch object previously returned by [`watchSub`](../watchsub)|
  |`refresh`||`Marker`|If present, requests the server returns the values of *all* points on the watch list, not just those which have changed|

  The grid body is not critical.

- **Response:** A grid with one or more rows with the following columns:

  |Column|Kind|Value Description|
  |------|----|-----------|
  |`id`|`Ref`|ID of a point in the watch list|
  |`curVal`|See `kind` tag of `point`|Value last read from the point, if known|
  |`curErr`|`Str`|Error message detail for non-"OK" states, see [`curErr`](https://www.project-haystack.org/tag/curErr)|
  |`curStatus`|`Str`|Status of the point being watched, see [`curStatus`](https://www.project-haystack.org/tag/curStatus)|

  If a presently-subscribed point is deleted from the asset model, the point's status will be updated to show unknown, indicating that the point no longer exists.  It is then the responsibility of the client to perform a [watchUnsub](../watchunsub) on this point to remove it from the watch.

## Examples:

### Changed points only


- **Request:**
  ```
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
- **Response:**
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
        "id": "r:a5f0c453-8125-4507-852f-1643d15efc07 pt3",
        "curStatus": "s:ok",
        "curVal": "n:83.7754"
      }
    ]
  }
  ```
### Fetch all points
- **Request:**
  ```
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

- **Response:**
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
