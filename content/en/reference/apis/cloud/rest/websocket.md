---
title: "Websocket subscription"
linkTitle: "websocket"
weight: 13
type: docs
description: >
    Receive real-time updates using websockets.
---

## Details

The traditional Project Haystack approach for real-time control is to use the [`watchPoll`](../ops/watchpoll) end-point, however this may lead to a poor user experience in some circumstances.  WideSky provides a websocket-based end-point which clients can subscribe to for receiving update notifications.  Clients are free to use either, or both methods for receiving updates as they see fit.

WideSky uses [`socket.io`](https://socket.io/) as a websocket abstraction layer.

### Connecting

**URL:** `https://example.on.widesky.cloud/${WATCH_ID}?Authorization=${ACCESS_TOKEN}`

where `${WATCH_ID}` is the ID of a Watch object created using [`watchSub`](../ops/watchsub) and `${ACCESS_TOKEN}` is the access token you use in regular requests (without the `Bearer ` prefix).

### Emitted Events

#### `pointData`

Emitted by the server whenever a point's value changes.  The body is a JSON object:

|Field|Type|Value Description|
|-----|----|-----------------|
|`id`|`Ref`|ID of the `point` that just changed|
|`curVal`|See `kind` tag of `point`|The last read value for the point|
|`curStatus`|`Str`|The state of the last read, see [`curStatus`](https://www.project-haystack.org/tag/curStatus)|
|`curErr`|`Str`|Associated error message if the read failed, see [`curErr`](https://www.project-haystack.org/tag/curErr), omitted if read successful.|

##### Example

```json
{
  "id": "r:d9afe4bc-79cb-11e8-84b1-0242ac120003",
  "curVal": "n:128.6915",
  "curStatus": "s:ok"
}
```
