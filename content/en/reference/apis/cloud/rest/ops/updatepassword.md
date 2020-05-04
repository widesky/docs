---
title: "Update Password"
linkTitle: "updatePassword"
weight: 16
type: docs
description: >
  Change the password of the currently logged-in user.
---
End users normally are not granted privileges for doing [`update`](../update) requests on their own `account` objects and so cannot directly change their passwords.  This end-point provides a simple means for a user to change the password for their account.

## Details

- **URL:** `/api/updatePassword`

- **Method:** `POST`

- **Request Data Params:** A JSON object with the following properties:

  |Property|Type|Value description|
  |------|----|-----------|
  |`password`|`string`|New user's password|

- **Response:** HTTP status code will be `200 OK` on success or `400 Bad Request` on failure.  Human-readable messages are given in plain text.

---

## Example

- **Request**
  ```
  POST /api/updatePassword HTTP/1.1
  Host: example.on.widesky.cloud
  Authorization: Bearer <authToken>
  Accept: application/json
  Content-Type: application/json

  {
      "newPassword": "let_me_in_now!"
  }
  ```

- **Response**
  ```
  Password updated.
  ```
