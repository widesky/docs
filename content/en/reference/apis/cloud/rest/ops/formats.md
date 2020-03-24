---
title: "Formats"
linkTitle: "formats"
weight: 3
type: docs
description: >
  Used to query which MIME types are available to read and write grids.
---

## Details

**URL:** `/api/formats`

**Method:** `GET`

**Request Data Params:** *None*

**Response:** *A grid where each row represents one supported MIME type with following columns:*

|Column|Value Description|
|------|-----------|
|`mime`|Str MIME type encoded as "mediaType/subType", these value must not include parameters. Any "text/" media type must be be encoded using UTF-8|
|`read`|Marker tag if server can read this format in requests (client can POST this format)|
|`write`|Marker tag if server can write this format in responses (client can request response in this format)|

## Example

**Request:**
```
GET /api/formats HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Bearer <authToken>
Accept: application/json
```
**Response:**
```json

{
  "meta": {
    "ver": "2.0"
  },
  "cols": [
    {
      "name": "mime"
    },
    {
      "name": "read"
    },
    {
      "name": "write"
    }
  ],
  "rows": [
    {
      "mime": "s:text/plain",
      "read": "m:",
      "write": "m:"
    },
    {
      "mime": "s:text/zinc",
      "read": "m:",
      "write": "m:"
    },
    {
      "mime": "s:text/csv",
      "write": "m:"
    },
    {
      "mime": "s:application/json",
      "read": "m:",
      "write": "m:"
    }
  ]
}
```
