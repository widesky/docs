---
title: "WideSky Query"
weight: 1
type: docs
description: Query data from WideSky using the GraphQL API.

---
## Overview
The WideSky Query node uses the GraphQL API to retrieve both timeseries and asset model information for use within a workflow.

![WideSky Query Node](/docs/images/edge/widesky-query-node.png)

## Inputs
*None*

## Outputs

|Path|Type|Description|
|----|----|-----------|
|`payload.response.data`|Object|The GraphQL response.|
|`payload.response.errors`|[String]|Error messages encountered during the query. Errors here normally indicate a partial success of the query.|
|`payload.request.to`|Number|An epoch representation of the `$to` option in UTC.|
|`payload.request.from`|Number|An epoch representation of the `$from` option in UTC.|
|`payload.request.query`|String|The requested GraphQL query.|

## Details

### Node properties
Property|Description|
|----|-----------|
|`WideSky server`|Configure the WideSky server to query. This configuration can be reused across all workflows|
|`$from`|Query start time alias value|
|`$to`|Query end time alias value|
|`query`|A (WideSky GraphQL query](../../../../reference/apis/cloud/graphql/).


{{% alert title="Tip"  color="primary" %}}
You can build a query using the [Grafana query buider](../../../cloud/vis/query-builder) first, and copy/paste it into the query property without modification.
{{% /alert %}}


### Time range alias
When querying for time series data, you can use the same relative range aliases (`$to` and `$from`) used by the Grafana query builder.

`$to` and `$from` both accept two input formats:

- A JavaScript date format e.g. `2015-03-25`
- A Grafana time unit e.g. `now - 24h`


### Relative Range
The following time units are supported: `s` (seconds), `m` (minutes), `h` (hours), `d` (days), `w` (weeks), `M` (months), `y` (years). The minus and plus operators allow you to step back or forward in time, relative to `now`. If you wish to display the full period of the unit (day, week, month, etc…), append `/$unit` to the end.

|Example Relative Range|From|To|
|----------------------|----|--|
|Last 5 minutes|`now-5m`|`now`|
|The day so far|`now/d`|`now`|
|This week|`now/w`|`now/w`|
|Week to date|`now/w`|`now`|
|Previous Month|`now-1M/M`|`now-1M/M`|

Adding a / suffix clamps the time unit to the start of that unit (in UTC). Note: Use the time offset to change this to your local time zone if needed.

|Use|Description|Example|
|---|-----------|-------|
|`/s`|Start of the second (00 sec)|`now - 1s/s`|
|`/m`|Start of the minute (00 min)|`now + 1m/m`|
|`/h`|Start of the hour (00m 00sec)|`now - 1h/h`|
|`/d`|Start of the day (12am)|`now + 1d/d`|
|`/M`|Start of the month (1st of month)|`now - 1M/M`|


## Example Usage

{{% alert title="Tip"  color="primary" %}}
- Copy the example flows to your clipboard and paste them using the Import dialogue.
- Remember to set the credentials of your WideSky server
{{% /alert %}}


### Query last 24h timeseries data
```text
[{"id":"c10faa9c.917728","type":"WideSky query","z":"d5894f.6e6b46b","name":"","server":"","from":"now","to":"now - 24h","timezone":"UTC","query":"haystack {\n  search(filter: \"point and his and tz and kind\", limit: 10) {\n    entity {\n      id\n      description\n      history(rangeAbsolute: {start: \"$from\", end: \"$to\"}) {\n        delta(groupBy: {groupByUnits: HOUR, groupBySize: 1, fill: NULLVALUE, aggregateFunction: MIN}) {\n          timeSeries {\n            dataPoints {\n              time\n              value\n            }\n          }\n        }\n      }\n    }\n  }\n}\n","x":380,"y":120,"wires":[["707b23cb.9ad42c","ac05e711.735f38","9d4a3082.cbea6","7c671e8a.0347a","9ff0988c.6a2ef8"]]},{"id":"54f16416.932ffc","type":"inject","z":"d5894f.6e6b46b","name":"Click to start flow","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":160,"y":120,"wires":[["c10faa9c.917728"]]},{"id":"707b23cb.9ad42c","type":"debug","z":"d5894f.6e6b46b","name":"Query from (epoch)","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.request.from","targetType":"msg","x":650,"y":200,"wires":[]},{"id":"ac05e711.735f38","type":"debug","z":"d5894f.6e6b46b","name":"Query to (epoch)","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.request.to","targetType":"msg","x":650,"y":240,"wires":[]},{"id":"9d4a3082.cbea6","type":"debug","z":"d5894f.6e6b46b","name":"Executed query","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.request","targetType":"msg","x":640,"y":280,"wires":[]},{"id":"a592e52a.14c188","type":"comment","z":"d5894f.6e6b46b","name":"Example: Query last 24h timeseries data","info":"","x":200,"y":60,"wires":[]},{"id":"7c671e8a.0347a","type":"debug","z":"d5894f.6e6b46b","name":"Response data","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.response.data","targetType":"msg","x":640,"y":120,"wires":[]},{"id":"9ff0988c.6a2ef8","type":"debug","z":"d5894f.6e6b46b","name":"Response errors","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.response.errors","targetType":"msg","x":640,"y":160,"wires":[]}]
```

### Query using a fixed datetime range

```text
[{"id":"76e7eebe.6b807","type":"inject","z":"d5894f.6e6b46b","name":"Start query","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":140,"y":420,"wires":[["5419fe2f.0a63"]]},{"id":"5419fe2f.0a63","type":"WideSky query","z":"d5894f.6e6b46b","name":"","server":"","from":"2020-01-10 00:00:00","to":"2020-02-10 00:00:00","timezone":"UTC","query":"haystack {\n  search(filter: \"point and his and tz and kind\", limit: 10) {\n    entity {\n      id\n      description\n      history(rangeAbsolute: {start: \"$from\", end: \"$to\"}) {\n        delta(groupBy: {groupByUnits: HOUR, groupBySize: 1, fill: NULLVALUE, aggregateFunction: MIN}) {\n          timeSeries {\n            dataPoints {\n              time\n              value\n            }\n          }\n        }\n      }\n    }\n  }\n}\n","x":340,"y":420,"wires":[["8e4473cd.ab5d1","9eebf5ee.931f48","c7403a4b.8ffe98","8f6e2004.202c6","e7b6b75f.495b88"]]},{"id":"53864ae3.9d0fe4","type":"comment","z":"d5894f.6e6b46b","name":"Example: Query using a fixed datetime range","info":"","x":210,"y":340,"wires":[]},{"id":"c7403a4b.8ffe98","type":"debug","z":"d5894f.6e6b46b","name":"Query from (epoch)","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.request.from","targetType":"msg","x":650,"y":500,"wires":[]},{"id":"8f6e2004.202c6","type":"debug","z":"d5894f.6e6b46b","name":"Query to (epoch)","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.request.to","targetType":"msg","x":650,"y":540,"wires":[]},{"id":"e7b6b75f.495b88","type":"debug","z":"d5894f.6e6b46b","name":"Executed query","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.request","targetType":"msg","x":640,"y":580,"wires":[]},{"id":"8e4473cd.ab5d1","type":"debug","z":"d5894f.6e6b46b","name":"Response data","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.response.data","targetType":"msg","x":640,"y":420,"wires":[]},{"id":"9eebf5ee.931f48","type":"debug","z":"d5894f.6e6b46b","name":"Response errors","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload.response.errors","targetType":"msg","x":640,"y":460,"wires":[]}]
```
