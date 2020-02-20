---
title: "About"
linkTitle: "about"
weight: 1
type: docs
description: Queries basic information about the server.
---

## Details

**URL:** `/api/about`

**Method:** `GET`

**Request Data Params:** *None*

**Response:** *Single row grid with following columns:*

|Column|Value Description|
|------|-----------|
|`haystackVersion`|Str version of REST implementation|
|`tz`|Str of server's default timezone|
|`serverName`|Str name of the server or project database|
|`serverTime`|Current DateTime of server's clock|
|`serverBootTime`|DateTime when server was booted up|
|`productName`|Str name of the server software product|
|`productUri`|Uri of the product's web site|
|`productVersion`|Str version of the server software product|
|`moduleName`|Module which implements Haystack server protocol if its a plug-in to the product|
|`moduleVersion`|Str version of moduleName|
|`vendorName`|Str name of the vendor|
|`VendorURL`|URI of the Vendors website|


---
### Example:
**Request:**
```
  GET /api/about HTTP/1.1
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
      "name": "haystackVersion"
    },
    {
      "name": "productName"
    },
    {
      "name": "productVersion"
    },
    {
      "name": "serverBootTime"
    },
    {
      "name": "serverName"
    },
    {
      "name": "serverTime"
    },
    {
      "name": "tz"
    },
    {
      "name": "vendorName"
    },
    {
      "name": "vendorUri"
    }
  ],
  "rows": [
    {
      "haystackVersion": "s:3.0",
      "productName": "s:WideSky",
      "productVersion": "s:20.03",
      "serverBootTime": "t:2020-01-01T00:00:00.000Z GMT",
      "serverName": "s:34136b9ba4f7",
      "serverTime": "t:2020-01-01T00:00:00.000Z GMT",
      "tz": "s:GMT",
      "vendorName": "s:WideSky",
      "vendorUri": "u:https://widesky.cloud"
    }
  ]
}
```
