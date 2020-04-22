---
title: "Impersonation"
weight: 3
type: docs
description: Impersonating another user
---

## Overview

The impersonation feature allows an authorised Widesky user to perform a REST operation based on its target user's permission settings. This is often used to verify permission settings.

## How it works

To be able to imitate another user, the HTTP header of the request must include an `X-IMPERSONATE` key, and its corresponding value will be the target user's ID.

The user performing the impersonation must have the `IMPERSONATE` permission in the WideSky `role`. That is, at least one of the associated `actionPolicies` in the WideSky `role` must carry the `IMPERSONATE` permission in the `permissions` list tag.

In addition, the impersonating user must also have the sufficient permission to do a `MODEL_READ` on the target user's entity model.

At the moment, WideSky's impersonation capability is not supported in the following REST APIs;

* Token request (`login`)
* Delete token (`logout`)
* Update password (`updatePassword`)

If an impersonate operation is successful then the HTTP response code relevant to the target operation is replied.

On situations where the impersonation operation fails then the caller is expected to receive the HTTP 400 (Bad request) code from the server.

For security reasons, the response from a failed impersonate request is deliberately set to a very brief "Cannot impersonate" message.

### Example request impersonating a user

```json
POST /api/read HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Bearer <authToken>
X-IMPERSONATE: b24bcb28-d0c3-4421-a4d1-4124e7e089c3
Accept: application/json
Content-Type: application/json

{
  "meta": {
    "ver": "2.0"
  },
  "cols": [
    {
      "name": "filter"
    },
    {
      "name": "limit"
    }
  ],
  "rows": [
    {
      "filter": "s:user",
      "limit": "n:0"
    }
  ]
}
```
