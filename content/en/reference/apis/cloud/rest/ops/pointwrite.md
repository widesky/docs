---
title: "Point Write"
linkTitle: "pointWrite"
weight: 15
type: docs
description: >
    Write a value to a `point` bearing the `writable` tag or view the last written value.
---

The `pointWrite` operation is used to write a new value, or view the last written value to a point, controlling the physical device linked to it. The control of the point is decided by a 17-level permissions system in which the numerically lowest "level" number has the highest priority (i.e. level 1 being highest, 17 being lowest). At this time, WideSky implements only the lowest-priority level (17).


{{% alert title="Notes"  color="primary" %}}
- Only writable real-time `point` entities (those bearing the `writable` tag) can be used with `pointWrite`.
- In the case of an error writing to the field device, the result will be reflected by the entities `writeStatus` and `writeErr` tags, which may be viewed by issuing a [`read`](../read) request.
{{% /alert %}}

## Details

- **URL:** `/api/pointWrite`

- **Method:** `POST`

- **Request Data Params (read last written value):** A grid with a single row with the following columns:

  |Column|Required|Kind|Value Description|
  |------|--------|----|-----------------|
  |`id`|✓|`Ref`|ID of the `point` to read last written value from|

- **Request Data Params (write new value):** A grid with a single row with the following columns:

  |Column|Required|Kind|Value Description|
  |------|--------|----|-----------------|
  |`id`|✓|`Ref`|ID of the `point` to write to|
  |`level`|✓|`Number`|Priority level to write to.  This **must** be set to `17`|
  |`val`|✓|See `kind` tag of `point` being written|The value to write to the point|
  |`who`|✓|`Str`|Name of the user or client writing|

  {{% alert title="Note"  color="primary" %}}
- If the entity carries an enum tag, `val` must be one of the enum values. e.g. on,off,start
- At this time, WideSky does not internally implement the `level` and `who` parameters in a `pointWrite`.  To remain compatible with Project Haystack's `pointWrite` operation, the `level` **must** be set to `17`, and the value of `who` is not presently recorded (it can be any value).
  {{% /alert %}}

- **Response (both types):** A grid with 17 rows and the following columns:

  |Column|Kind|Value Description|
  |------|----|-----------------|
  |`level`|`Number`|Priority level|
  |`levelDis`|`Str`|Description of the priority level|
  |`who`|`Str`|Name of the user or client writing|
  |`val`|See `kind` tag of `point` in request|The value last written to the `point`|

  {{% alert title="Note"  color="primary" %}}
  For Project Haystack compatibility, all 17 levels are reported, but only level 17 has meaningful data.  `who` is always reported as `SYSTEM`, as that information is not recorded.
  {{% /alert %}}

## Examples:
### Read last written value

- **Request:**
  ```
  POST /api/pointWrite HTTP/1.1
  Host: example.on.widesky.cloud
  Authorization: Bearer <authToken>
  Accept: application/json
  Content-Type: application/json

  {
   "meta": {
    "ver": "2.0"
   },
   "cols": [
    {
     "name": "id"
    }
   ],
   "rows": [
    {
     "id": "r:0eb5f7d4-0243-441a-9e29-8695112d9e54"
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
     "name": "level"
    },
    {
     "name": "levelDis"
    },
    {
     "name": "val"
    },
    {
     "name": "who"
    }
   ],
   "rows": [
    {
     "level": "n:1",
     "levelDis": "s:1: Override"
    },
    {
     "level": "n:2",
     "levelDis": "s:2"
    },
    {
     "level": "n:3",
     "levelDis": "s:3"
    },
    {
     "level": "n:4",
     "levelDis": "s:4"
    },
    {
     "level": "n:5",
     "levelDis": "s:5"
    },
    {
     "level": "n:6",
     "levelDis": "s:6"
    },
    {
     "level": "n:7",
     "levelDis": "s:7"
    },
    {
     "level": "n:8",
     "levelDis": "s:8: Timer Override"
    },
    {
     "level": "n:9",
     "levelDis": "s:9"
    },
    {
     "level": "n:10",
     "levelDis": "s:10"
    },
    {
     "level": "n:11",
     "levelDis": "s:11"
    },
    {
     "level": "n:12",
     "levelDis": "s:12"
    },
    {
     "level": "n:13",
     "levelDis": "s:13"
    },
    {
     "level": "n:14",
     "levelDis": "s:14"
    },
    {
     "level": "n:15",
     "levelDis": "s:15"
    },
    {
     "level": "n:16",
     "levelDis": "s:16"
    },
    {
     "level": "n:17",
     "levelDis": "s:17: Default",
     "val": "n:1",
     "who": "s:SYSTEM"
    }
   ]
  }
  ```

### Write a new value

- **Request:**
  ```
  POST /api/pointWrite HTTP/1.1
  Host: example.on.widesky.cloud
  Authorization: Bearer <authToken>
  Accept: application/json
  Content-Type: application/json

  {
   "meta": {
    "ver": "2.0"
   },
   "cols": [
    {
     "name": "id"
    },
    {
     "name": "level"
    },
    {
     "name": "who"
    },
    {
     "name": "val"
    }
   ],
   "rows": [
    {
     "id": "r:0eb5f7d4-0243-441a-9e29-8695112d9e54",
     "level": "n:17",
     "val": "n:0",
     "who": "s:Johnny Citizen"
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
     "name": "level"
    },
    {
     "name": "levelDis"
    },
    {
     "name": "val"
    },
    {
     "name": "who"
    }
   ],
   "rows": [
    {
     "level": "n:1",
     "levelDis": "s:1: Override"
    },
    {
     "level": "n:2",
     "levelDis": "s:2"
    },
    {
     "level": "n:3",
     "levelDis": "s:3"
    },
    {
     "level": "n:4",
     "levelDis": "s:4"
    },
    {
     "level": "n:5",
     "levelDis": "s:5"
    },
    {
     "level": "n:6",
     "levelDis": "s:6"
    },
    {
     "level": "n:7",
     "levelDis": "s:7"
    },
    {
     "level": "n:8",
     "levelDis": "s:8: Timer Override"
    },
    {
     "level": "n:9",
     "levelDis": "s:9"
    },
    {
     "level": "n:10",
     "levelDis": "s:10"
    },
    {
     "level": "n:11",
     "levelDis": "s:11"
    },
    {
     "level": "n:12",
     "levelDis": "s:12"
    },
    {
     "level": "n:13",
     "levelDis": "s:13"
    },
    {
     "level": "n:14",
     "levelDis": "s:14"
    },
    {
     "level": "n:15",
     "levelDis": "s:15"
    },
    {
     "level": "n:16",
     "levelDis": "s:16"
    },
    {
     "level": "n:17",
     "levelDis": "s:17: Default",
     "val": "n:0",
     "who": "s:SYSTEM"
    }
   ]
  }
  ```
