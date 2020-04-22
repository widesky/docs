---
title: "Authentication"
linkTitle: "Authentication"
weight: 1
type: docs
Description: Authentication via OAuth2
---

Both WideSky Cloud GraphQL and REST APIs use JSON-based OAuth2 authentication. This section describes how to get a token for subsequent REST or GraphQL calls.

You should have been issued with a `username` and `password` for your user account, along with a `clientId` and `clientSecret` for your client application. The `clientSecret` should be treated like a password and be stored securely.

## Authentication Steps
1. Send both the user's and client application's information to the `token` operation. This operation grants the client application an `accessToken` and `refreshToken`.
2. The accessToken can then be used to make subsequent API requests by specifying `Bearer <accessToken>` in the authorization header of the request.
3. The `accessToken` is valid for 7 days. After the `accessToken` has expired, you can either request another one the same way by sending the user's information again, or send the `refreshToken` that was received in the initial request.
{{% alert title="Tip" %}}
The refresh method is preferred as you don't have to save the user's sensitive information.
{{% /alert %}}

## Details

**URL:** `/oauth2/token`

**Method:** `POST`

**Header Parameters:** To identify the client accessing the API resource, include the `clientId` and `clientSecret` in the header with the following format:

```
Authorization: Basic <base64 encoded string consisting of "<clientId>:<clientSecret>"
```

**Request Data Params (request access token):**
```
grant_type: literal string "password"
username: email address of the user account
password: characters to prove the identity of the user
```

**Request Data Params (refresh access token):**
```
grant_type: literal string "refresh_token"
refresh_token: a previously obtained refresh token
```

**Response:**
```
access_token: A token that may be used to perform authenticated requests on behalf of the user
refresh_token: A token which may be used to acquire a new access_token
expires_in: The number of milliseconds until the access token will expire
token_type: The literal string "Bearer"
```

## Example

**Authorization Header:**

If your credentials are:

* `clientId`: `myCoolApp`
* `clientSecret`: `password1234`

then you should take the string `myCoolApp:password1234` and encode it using Base64, giving you:

```
bXlDb29sQXBwOnBhc3N3b3JkMTIzNA==
```

Your Authorization header would therefore look like this:

```
Authorization: Basic bXlDb29sQXBwOnBhc3N3b3JkMTIzNA==
```

Some HTTP clients will do this for you if you tell them to use [HTTP Basic authentication](https://tools.ietf.org/html/rfc2617#section-2) and specify `clientId` for the `username` field and `clientSecret` for the `password`, e.g. in [`curl`](https://curl.haxx.se/):

```
$ curl -u myCoolApp:password1234 \
       -H "Accept: application/json" \
       -H "Content-Type: application/json" \
       -XPOST -d '{… see examples below …}' \
       https://example.on.widesky.cloud/widesky/oauth2/token
```

**Request (access token):**
```
POST /oauth2/token HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Basic <base64 encoded string of clientId and clientSecret>
Accept: application/json
Content-Type: application/json

{
    "grant_type": "password",
    "username": "demo@example.com",
    "password": "demopassword"
}
```

**Request (refresh token):**
```
POST /oauth2/token HTTP/1.1
Host: example.on.widesky.cloud
Authorization: Basic <base64 encoded string of clientId and clientSecret>
Accept: application/json
Content-Type: application/json

{
    "grant_type": "refresh_token",
    "refresh_token": "rXltx0DynvQksGaeMgcdv1Y8..."
}
```

**Response:**
```json
{
  "access_token": "MG2DLJT0I4DTmHmOFwcd9...",
  "refresh_token": "rXltx0DynvQksGaeMgcdv1Y8...",
  "expires_in": 1470633701863,
  "token_type": "Bearer"
}
```
