---
title: "Watch Unsubscribe"
linkTitle: "watchUnsub"
weight: 14
type: docs
description: >
    Close a "watch" list completely, or remove `point`s bearing the `cur` tag.
---

The `watchUnsub` operation is used for removing entities or closing a watch that was previously created by the [`watchSub`](../watchsub) op.

Only real-time `point`s (those bearing the `cur` tag) can be used with a watch, any point lacking the `cur` tag will be ignored.

## Details
- **URL:** `/api/watchUnsub`

- **Method:** `POST`

- **Request Data Params (close a watch):** A grid with the following metadata fields:

  |Meta Field|Required|Kind|Value Description|
  |------|--|--|-----------|
  |`watchId`|✓|`Str`|ID of the watch previously returned by [`watchSub`](../watchsub)|
  |`close`||`Marker`|Close the watch. By including this marker, you are indicating to the server that the watch should be closed.|

  The grid body is not critical


  {{% alert title="Tip"  color="primary" %}}
The watch will only be closed if no other clients are subscribed to it.
  {{% /alert %}}



- **Request Data Params (remove from watch):**
  - A grid with the following metadata fields:

    |Meta Field|Required|Kind|Value Description|
    |------|--|--|-----------|
    |`watchId`|✓|`Str`|The ID of the watch object previously returned by [`watchSub`](../watchsub)|

  - With one or more rows with the following columns:

    |Column|Required|Kind|Value Description|
    |------|---|-|-----------|
    |`id`|*one or more*|`Ref`|Point to be removed from the watch|

    {{% alert title="Tip"  color="primary" %}}
When removing points only (i.e. not closing the watch), the watchId remains unchanged.
    {{% /alert %}}

- **Response (both types):** An empty grid.

---
## Examples:

### Close watch
- **Request:**
  ```
  POST /api/watchUnsub HTTP/1.1
  Host: example.on.widesky.cloud
  Authorization: Bearer <authToken>
  Accept: application/json
  Content-Type: application/json

  {
    "meta": {
      "ver": "2.0",
      "watchId": "s:0255e1c9-519f-4630-bf0e-9bd99b221109",
      "close": "m:"
    },
    "cols": [
      {
        "name": "empty"
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
        "name": "empty"
      }
    ],
    "rows": []
  }
  ```
### Append to watch
- **Request:**
  ```
  POST /api/watchUnsub HTTP/1.1
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
        "id": "r:site.equip2.pt4 pt4"
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
