---
title: "Watch Unsubscribe"
linkTitle: "watchUnsub"
weight: 14
type: docs
description: >
    Close a "watch" list completely, or remove `point`s bearing the `cur` tag.
---

## Details

The `watchUnsub` operation is used for removing points from or closing a watch.   [Watches](http://project-haystack.org/doc/Rest#watches) are a mechanism used to provide real-time updates to a Project Haystack client by way of a simple polling-based HTTP API.

Only real-time `point`s (those bearing the `cur` tag) can be used with a watch, any point lacking the `cur` tag will be ignored.

**URL:** `/api/watchUnsub`

**Method:** `POST`

**Request Data Params (close a watch):** *A grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`watchId`|`Str`|ID of the watch previously returned by `watchSub`|
|`close`|`Marker`|Close the watch.  By including this marker, you are indicating to the server that the watch should be closed.|

*… the grid body is not critical*

**Request Data Params (remove from watch):** *A grid with the following metadata fields:*

|Field|Kind|Value Description|
|------|----|-----------|
|`watchId`|`Str`|The ID of the watch object previously returned by `watchSub`|

*… and one or more rows with the following columns:*

|Column|Kind|Value Description|
|------|----|-----------|
|`id`|`Ref`|Point to be removed from the watch|

**Response (both types):** *An empty grid.*

---
### Examples:

**Request (close watch):**
```json
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

**Request (append to watch):**
```json
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
