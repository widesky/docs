---
title: "WideSky Alarm"
weight: 1
type: docs
description: How to create a rules based alarm using WideSky Cloud and WideSky Edge
---

## Problem
You have a energy metering IoT solution with hundreds of energy meters reporting to WideSky and you want to alarm for "high usage" events for any metered area. As the definition of "high usage" vaires for each meter, the alarm needs consider the previous history to determine anomolous usage.

## Solution Overview
For this guide we'll demonstrate using the analytics functions and data processing function to create a single alarm flow for all energy meters the meet the specific conditions. Examples dashboards and WideSky Edge flows are below so you can eaily import into your own project.


## Assumptions
### Asset Model
- Every tenant is a `space` entity
- Each meter is an `equip` entity with the following tags:
  - `device`
  - `meter`
  - `elec`
  - `spaceRef` to a `space` entity
- Each meter has 1 `point` entity with the following tags:
  - `his`
  - `kind`
  - `energy`
  - `hisTotalised`
- The point is updated with a new reading every hours

## Details

### Node properties
Property|Description|
|----|-----------|
|`WideSky server`|Configure the WideSky server to query. This configuration can be reused across all workflows|
|`Alarm conditions`|A list of [conditions](./#conditions) to match. |
|`dis`|Value of the `dis` tag on the alarm entity|
|`name`|Value of the `name` tag on the alarm entity|


{{% alert title="Tip"  color="primary" %}}
You can change the `dis` and `name` values; they will be updated on the alarm entity when the flow is executed.
{{% /alert %}}


### Conditions
A condition is a user-definable rule for setting the alarm severity. By default, if none of the user-defined conditions trigger the alarm level is set to 0.

{{% alert title="Note"  color="warning" %}}
It is recommended that the following alarm severity levels be used: 0 being Off, 1 = most severe, and 255 the least severe.
{{% /alert %}}


### New Alarm Entity
For each WideSky entity that is used as a time series data source, the alarm node will create a new WideSky entity for writing the resulting alarm severity time series to. Upon creation, it will:
- Link the new entity to its source entity via the `alarmOf` ref tag
- Add the `alarm` marker tag
- Link to the parent `equip` entity of the source entity via the `equipRef` tag
- Match the source entity `tz` value
- Add the `edgeNodeId` tag to match its `id`
- Map the `kind` tag to `Number` to accept the calculated severity level time series

```hsgrid-json
{
"_options": {
    "dump": false,
    "omitTags": [],
    "highlightEntities": ["@GHI"],
    "highlightTags": ["alarm"],
    "entityClasses": {},
    "tagClasses": {},
    "styles": []
},
"rows":[

   {
      "id":"r:ABC",
      "dis":"Meter 1",
      "equip":"m:"
   },
   {
      "id":"r:DEF",
      "dis":"s:Energy (source entity)",
      "point":"m:",
      "equipRef":"r:ABC",
      "kind":"s:Number",
      "his":"m:",
      "tz":"s:GMT-10"
   },
   {
      "id":"r:GHI",
      "dis":"s:New alarm entity",
      "point":"m:",
      "equipRef":"r:ABC",
      "kind":"s:Number",
      "alarmOf":"r:DEF",
      "alarm":"m:",
      "his":"m:",
      "edgeNodeId":"s:299b3e91.279c8a",
      "tz":"s:GMT-10"
   }
]}
```

## Example Usage

{{% alert title="Tip"  color="primary" %}}
Copy the example flows to your clipboard and paste them using the Import dialogue.
{{% /alert %}}


### Alarm on multiple entities
```text
[{"id":"51fa2a24.5a6544","type":"comment","z":"d363e2d2.5a7c","name":"Multiple alarm example","info":"","x":120,"y":60,"wires":[]},{"id":"bd906116.c7b9c","type":"WideSky query","z":"d363e2d2.5a7c","name":"","server":"","from":"now-25h","to":"now-1h","timezone":"UTC","query":"haystack {\n  search(filter: \"point and his\", limit:3) {\n    entity {\n      id\n      history(rangeAbsolute: {start: \"$from\", end: \"$to\"}) {\n        time series {\n          dataPoints {\n            time\n            value\n          }\n        }\n      }\n    }\n  }\n}\n","x":300,"y":120,"wires":[["8fade366.310e8"]]},{"id":"8fade366.310e8","type":"change","z":"d363e2d2.5a7c","name":"set entities to msg.payload","rules":[{"t":"set","p":"payload","pt":"msg","to":"payload.response.data.haystack.search.entity","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":540,"y":120,"wires":[["fe560cab.7c8c2"]]},{"id":"fe560cab.7c8c2","type":"split","z":"d363e2d2.5a7c","name":"split each entity","splt":"\\n","spltType":"str","arraySplt":1,"arraySpltType":"len","stream":true,"addname":"payload","x":560,"y":160,"wires":[["32c7fa87.459316"]]},{"id":"32c7fa87.459316","type":"WideSky alarm","z":"d363e2d2.5a7c","name":"","server":"e74429ba.44cc98","rules":[{"t":"gt","v":"100","vt":"num","level":"5"}],"outputs":1,"alarmName":"test_alarm","alarmDis":"Test alarm","x":820,"y":120,"wires":[["a7f49585.ac06f8"]]},{"id":"a7f49585.ac06f8","type":"debug","z":"d363e2d2.5a7c","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","x":1010,"y":120,"wires":[]},{"id":"c783f8a9.c99e28","type":"inject","z":"d363e2d2.5a7c","name":"Click to start flow","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":120,"y":120,"wires":[["bd906116.c7b9c"]]}]
```
