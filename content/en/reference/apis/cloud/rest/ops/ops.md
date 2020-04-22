---
title: "Ops"
linkTitle: "ops"
weight: 2
type: docs
description: >
  Queries which operations are available on the server.
---

## Details

- **URL:** `/api/ops`

- **Method:** `GET`

- **Request Data Params:** *None*

- **Response:** Single row grid with following columns:

  |Column|Kind|Value Description|
  |------|----|-----------|
  |`name`|`Str`|Name of the operation in the URI namespace|
  |`summary`|`Str`|Short description of the operation|

## Example

- **Request:**
  ```
  GET /api/ops HTTP/1.1
  Host: example.on.widesky.cloud
  Authorization: Bearer <authToken>
  Accept: application/json
  ```
- **Response:**
  ```
  {
    "meta": {
      "ver": "2.0"
    },
    "cols": [
      {
        "name": "name"
      },
      {
        "name": "summary"
      }
    ],
    "rows": [
      {
        "name": "s:about",
        "summary": "s:Summary information for server"
      },
      {
        "name": "s:ops",
        "summary": "s:Operations supported by this server"
      },
      {
        "name": "s:formats",
        "summary": "s:Grid data formats supported by this server"
      },
      {
        "name": "s:read",
        "summary": "s:Read entity records in database"
      },
      {
        "name": "s:hisRead",
        "summary": "s:Read time series from historian"
      },
      {
        "name": "s:hisWrite",
        "summary": "s:Write time series data to historian"
      },
      {
        "name": "s:createRec",
        "summary": "s:Create new rec(s) to the Haystack server."
      },
      {
        "name": "s:updateRec",
        "summary": "s:Modify existing rec(s) on the Haystack Server."
      },
      {
        "name": "s:deleteRec",
        "summary": "s:Remove rec(s) from the Haystack Server."
      }
    ]
  }
  ```
