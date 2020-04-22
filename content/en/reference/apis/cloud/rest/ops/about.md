---
title: "About"
linkTitle: "about"
weight: 1
type: docs
description: Queries basic information about the server.
---

## Details

- **URL:** `/api/about`

- **Method:** `GET`

- **Request Data Params:** *None*

- **Response:** Single row grid with following columns:

  |Column|Kind|Value Description|
  |------|----|-----------|
  |`haystackVersion`|`Str`|Version of REST implementation|
  |`tz`|`Str`|Server's default timezone|
  |`serverName`|`Str`|Name of the server or project database|
  |`serverTime`|`DateTime`|Current Date/Time of server's clock|
  |`serverBootTime`|`DateTime`|Date/Time when server was booted up|
  |`productName`|`Str`|Name of the server software product|
  |`productUri`|`Uri`|URL of the product's web site|
  |`productVersion`|`Str`|Version of the server software product|
  |`moduleName`|`Str`|Module which implements Haystack server protocol if its a plug-in to the product|
  |`moduleVersion`|`Str`|Version of module|
  |`vendorName`|`Str`|Name of the vendor|
  |`VendorURL`|`Uri`|URI of the Vendor's website|


---
### Example:
- **Request:**
  ```
    GET /api/about HTTP/1.1
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
