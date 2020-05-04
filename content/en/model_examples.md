---
title: "Model Examples"
weight: 4
type: docs
description: >
  Example not for publishing
menu:
  main:
    weight: 5
index_disable: true
breadcrumb_disable: true
d3graphviz: true
draft: true
---

Example `graphviz` diagrams to show it can be done.


## Example 1 - FQName
```hsgrid-json
{
"_options": {
    "dump": false,
    "omitTags": [],
    "highlightTags": ["name"],
    "entityClasses": {},
    "tagClasses": {},
    "styles": []
},
"rows":[
   {
      "id":"r:ABC",
      "dis":"s:WideSky Site",
      "site":"m:",
      "name":"s:ws",
      "fqname":"s:ws"
   },
   {
      "id":"r:DEF",
      "dis":"Meter 1",
      "equip":"m:",
      "siteRef":"r:ABC",
      "name":"s:meter",
      "fqname":"s:ws.meter"
   },
   {
      "id":"r:GHI",
      "dis":"s:Energy",
      "point":"m:",
      "equipRef":"r:DEF",
      "siteRef":"r:ABC",
      "name":"s:energy",
      "kind":"s:Number",
      "fqname":"s:ws.meter.energy"
   },
   {
      "id":"r:JKL",
      "dis":"Meter 1",
      "equip":"m:",
      "siteRef":"r:ABC",
      "name":"s:meter 2",
      "fqname":"s:ws.meter2"
   },
   {
      "id":"r:MNO",
      "dis":"s:Energy",
      "point":"m:",
      "equipRef":"r:JKL",
      "siteRef":"r:ABC",
      "name":"s:energy",
      "kind":"s:Number",
      "fqname":"s:ws.meter2.energy"

   }
]}
```












## Other expriments are below, don't follow these...
```hsgrid-json
{
"_options": {
    "dump": true,
    "omitTags": [
        "wsgServiceConfig"
    ],
    "entityClasses": {
        "site": "wsEntitySite",
        "equip": "wsEntityEquip",
        "point": "wsEntityPoint"
    },
    "tagClasses": {
        "id": "wsTagId",
        "dis": "wsTagDis"
    },
    "styles": [
    ]
},
"meta": {"ver":"2.0"},
"cols":[{"name":"id"}, {"name":"device"}, {"name":"dis"}, {"name":"edgeNodeId"}, {"name":"equip"}, {"name":"equipRef"}, {"name":"fqname"}, {"name":"his"}, {"name":"kind"}, {"name":"lastHisTime"}, {"name":"lastHisVal"}, {"name":"name"}, {"name":"point"}, {"name":"site"}, {"name":"siteRef"}, {"name":"tz"}, {"name":"wsgHistoricalInterval"}, {"name":"wsgHistoricalOffset"}, {"name":"wsgServiceConfig"}, {"name":"wshEui64"}, {"name":"wshFirmwareVer"}, {"name":"wshPoint"}, {"name":"wshRTLifetime"}, {"name":"wshRTTimeout"}],
"rows":[
{"id":"r:db866e5d-0b16-4be7-aaea-2376485538fb backfill_count", "dis":"s:backfill_count", "equipRef":"r:be4cc43c-86d8-4167-9642-07d8f8ea3475 Hub #9 (7b54)", "fqname":"s:ws.hub7b54.backfill_count", "his":"m:", "kind":"s:Number", "lastHisTime":"t:2020-04-28T09:40:00Z", "lastHisVal":"n:0", "name":"s:backfill_count", "point":"m:", "siteRef":"r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub \\\"Test Site\\\"", "tz":"s:UTC", "wsgServiceConfig":"s:type: backfill_count\n", "wshPoint":"n:10"},
{"id":"r:6d320af3-c392-4fd5-875f-289ce16f4b9b backfill_lag", "dis":"s:backfill_lag", "equipRef":"r:be4cc43c-86d8-4167-9642-07d8f8ea3475 Hub #9 (7b54)", "fqname":"s:ws.hub7b54.backfill_lag", "his":"m:", "kind":"s:Number", "lastHisTime":"t:2020-04-28T07:38:00Z", "lastHisVal":"n:120", "name":"s:backfill_lag", "point":"m:", "siteRef":"r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub \\\"Test Site\\\"", "tz":"s:UTC", "wsgServiceConfig":"s:type: backfill_lag\n", "wshPoint":"n:4"}
]}
```
```d3gv-dot
/*{
    "styles": [
        {
            "selector": "#site > polygon",
            "attr": {
                "fill": "rgb(192, 224, 252)"
             }
        },
        {
            "selector": "#a_site_id > a > text",
            "attr": {
                "fill": "rgb(255, 0, 0)"
            }
        }
    ]
}*/
digraph D {
  node [shape=plaintext style=filled margin=0 fontname="Arial" fontsize="8"];
    rankdir=RL;
  elecMeter [shape=plaintext style=solid];
  site [ id="site" label=<
   <table border="0" cellborder="0" cellspacing="0">
    /* href="#" is a work-around to a bug in Graphviz */
    <tr><td align="left" id="site_id" href="#">id: @2180b666-430b2363</td></tr>
    <tr><td align="left">site</td></tr>
    <tr><td align="left">dis: 'Gaithersburg'</td></tr>
    <tr><td align="left">geoAddr: '18212 Montgomery Village Ave' </td></tr>
    <tr><td align="left">geoCity: 'Gaithersburg'</td></tr>
    <tr><td align="left">geoCoord: C(39.154824,-77.209002)</td></tr>
    <tr><td align="left">geoCountry: 'US'</td></tr>
    <tr><td align="left">geoPostalCode: '20879'</td></tr>
    <tr><td align="left">geoState: 'MD'</td></tr>
    <tr><td align="left">tz: 'New_York'</td></tr>
   </table>>];
  equip1 [ label=<
   <table border="0" cellborder="0" cellspacing="0">
    <tr><td align="left">id: @2180b666-7032054c</td></tr>
    <tr><td align="left">equip</td></tr>
    <tr><td align="left">dis: 'RTU-1'</td></tr>
    <tr><td align="left">ahu</td></tr>
    <tr><td align="left">hvac</td></tr>
    <tr><td align="left">rooftop</td></tr>
    <tr><td align="left" port='siteRef'>siteRef: @2180b666-430b2363</td></tr>
    <tr><td align="left" port ='elecMeterRef'>elecMeterRef: @2180b666-7032054d</td></tr>
    <tr><td align="left" port ='spaceRef'> spaceRef: @2180b666-7032054d</td></tr>
   </table>>];
  point1[ label=<
   <table border="0" cellborder="0" cellspacing="0">
    <tr><td align="left">id: @218a0616-0b5e382b</td></tr>
    <tr><td align="left">point</td></tr>
    <tr><td align="left">dis: 'Discharge air temperature'</td></tr>
    <tr><td align="left">sensor</td></tr>
    <tr><td align="left">air</td></tr>
    <tr><td align="left">temp</td></tr>
    <tr><td align="left">discharge</td></tr>
    <tr><td align="left">his</td></tr>
    <tr><td align="left">unit:'°F'</td></tr>
    <tr><td align="left" port='equipRef'>equipRef: @2180b666-7032054c</td></tr>
    <tr><td align="left" port='siteRef'>siteRef: @2180b666-430b2363</td></tr>
   </table>>];
point2[ label=<
   <table border="0" cellborder="0" cellspacing="0">
    <tr><td align="left">id: @218a0616-0b5e382b</td></tr>
    <tr><td align="left">point</td></tr>
    <tr><td align="left">dis: 'Discharge air temperature'</td></tr>
    <tr><td align="left">sensor</td></tr>
    <tr><td align="left">air</td></tr>
    <tr><td align="left">temp</td></tr>
    <tr><td align="left">discharge</td></tr>
    <tr><td align="left">his</td></tr>
    <tr><td align="left">unit:'°F'</td></tr>
    <tr><td align="left" port='equipRef'>equipRef: @2180b666-7032054c</td></tr>
    <tr><td align="left" port='siteRef'>siteRef: @2180b666-430b2363</td></tr>
   </table>>];
  equip2 [ label=<
   <table border="0" cellborder="0" cellspacing="0">
    <tr><td align="left">id: @2180b666-7032054c</td></tr>
    <tr><td align="left">equip</td></tr>
    <tr><td align="left">dis: 'RTU-1'</td></tr>
    <tr><td align="left">ahu</td></tr>
    <tr><td align="left">hvac</td></tr>
    <tr><td align="left">rooftop</td></tr>
    <tr><td align="left" port='siteRef'>siteRef: @2180b666-430b2363</td></tr>
    <tr><td align="left" port ='elecMeterRef'>elecMeterRef: @2180b666-7032054d</td></tr>
    <tr><td align="left" port ='spaceRef'> spaceRef: @2180b666-7032054d</td></tr>
   </table>>];
  point3[ label=<
   <table border="0" cellborder="0" cellspacing="0">
    <tr><td align="left">id: @218a0616-0b5e382b</td></tr>
    <tr><td align="left">point</td></tr>
    <tr><td align="left">dis: 'Discharge air temperature'</td></tr>
    <tr><td align="left">sensor</td></tr>
    <tr><td align="left">air</td></tr>
    <tr><td align="left">temp</td></tr>
    <tr><td align="left">discharge</td></tr>
    <tr><td align="left">his</td></tr>
    <tr><td align="left">unit:'°F'</td></tr>
    <tr><td align="left" port='equipRef'>equipRef: @2180b666-7032054c</td></tr>
    <tr><td align="left" port='siteRef'>siteRef: @2180b666-430b2363</td></tr>
   </table>>];
point4[ label=<
   <table border="0" cellborder="0" cellspacing="0">
    <tr><td align="left">id: @218a0616-0b5e382b</td></tr>
    <tr><td align="left">point</td></tr>
    <tr><td align="left">dis: 'Discharge air temperature'</td></tr>
    <tr><td align="left">sensor</td></tr>
    <tr><td align="left">air</td></tr>
    <tr><td align="left">temp</td></tr>
    <tr><td align="left">discharge</td></tr>
    <tr><td align="left">his</td></tr>
    <tr><td align="left">unit:'°F'</td></tr>
    <tr><td align="left" port='equipRef'>equipRef: @2180b666-7032054c</td></tr>
    <tr><td align="left" port='siteRef'>siteRef: @2180b666-430b2363</td></tr>
   </table>>];
space[ label=<
   <table border="0" cellborder="0" cellspacing="0">
    <tr><td align="left">id: @218a0616-0b5e382b</td></tr>
    <tr><td align="left">space</td></tr>
    <tr><td align="left">dis: 'A large space'</td></tr>
    <tr><td align="left" port='siteRef'>siteRef: @2180b666-430b2363</td></tr>
   </table>>];
    point1:equipRef        -> equip1;
    point1:siteRef        -> site;
    equip1:siteRef          -> site;
    point2:equipRef        -> equip1;
    point2:siteRef        -> site;
    point3:equipRef        -> equip2;
    point3:siteRef        -> site;
    equip2:siteRef          -> site;
    point4:equipRef        -> equip2;
    point4:siteRef        -> site;
    space:siteRef       -> site;
    equip1:spaceRef     -> space;
    equip2:spaceRef     -> space;
    equip1:elecMeterRef -> elecMeter;
    equip2:elecMeterRef -> elecMeter;
}
```

An attempt at a WideSky asset model diagram

```hsgrid-json
{
"_options": {
    "dump": true,
    "omitTags": [
        "wsgServiceConfig"
    ],
    "entityClasses": {
        "site": "wsEntitySite",
        "equip": "wsEntityEquip",
        "point": "wsEntityPoint"
    },
    "tagClasses": {
        "id": "wsTagId",
        "dis": "wsTagDis"
    },
    "styles": [
        {
            "selector": "#r0 > polygon",
            "attr": {
                "fill": "rgb(192, 224, 252)"
             }
        },
        {
            "selector": "#a_r0_id > a > text",
            "attr": {
                "fill": "rgb(255, 200, 0)"
            }
        }
    ]
},
"meta": {"ver":"2.0"},
"cols":[{"name":"id"}, {"name":"device"}, {"name":"dis"}, {"name":"edgeNodeId"}, {"name":"equip"}, {"name":"equipRef"}, {"name":"fqname"}, {"name":"his"}, {"name":"kind"}, {"name":"lastHisTime"}, {"name":"lastHisVal"}, {"name":"name"}, {"name":"point"}, {"name":"site"}, {"name":"siteRef"}, {"name":"tz"}, {"name":"wsgHistoricalInterval"}, {"name":"wsgHistoricalOffset"}, {"name":"wsgServiceConfig"}, {"name":"wshEui64"}, {"name":"wshFirmwareVer"}, {"name":"wshPoint"}, {"name":"wshRTLifetime"}, {"name":"wshRTTimeout"}],
"rows":[
{"id":"r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub \\\"Test Site\\\"", "dis":"s:WideSky Hub \"Test Site\"", "fqname":"s:ws", "name":"s:ws", "site":"m:"},
{"id":"r:be4cc43c-86d8-4167-9642-07d8f8ea3475 Hub #9 (7b54)", "device":"m:", "dis":"s:Hub #9 (7b54)", "equip":"m:", "fqname":"s:ws.hub7b54", "name":"s:hub7b54", "siteRef":"r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub \\\"Test Site\\\"", "tz":"s:GMT-10", "wsgHistoricalInterval":"n:120", "wsgHistoricalOffset":"n:0", "wsgServiceConfig":"s:update:\n      config_int: 60\n      firmware_int: 60\n      block_sz: 256\nconsole:\n      baud: 115200\n      parity: N\n      bytesize: 8\n      stopbits: 1\n      timeout_mode: console\n      flow_control: none\n      parity_err: discard\n      rx_port: 2\n      tx_port: 1\nsyslog:\n      level: 3\n      persist: 0", "wshEui64":"s:00124b0011f47b54", "wshFirmwareVer":"s:1.3.4-alpha.26+200320T0732-ce075f89", "wshRTLifetime":"n:300", "wshRTTimeout":"n:60"},
{"id":"r:4fa1144d-38b7-4a4b-bb07-566fbbef00cd Uptime", "dis":"s:Uptime", "equipRef":"r:be4cc43c-86d8-4167-9642-07d8f8ea3475 Hub #9 (7b54)", "fqname":"s:ws.hub7b54.uptime", "his":"m:", "kind":"s:Number", "lastHisTime":"t:2020-04-28T09:40:00Z", "lastHisVal":"n:120071", "name":"s:uptime", "point":"m:", "siteRef":"r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub \\\"Test Site\\\"", "tz":"s:UTC", "wsgServiceConfig":"s:type: uptime\n", "wshPoint":"n:3"},
{"id":"r:db866e5d-0b16-4be7-aaea-2376485538fb backfill_count", "dis":"s:backfill_count", "equipRef":"r:be4cc43c-86d8-4167-9642-07d8f8ea3475 Hub #9 (7b54)", "fqname":"s:ws.hub7b54.backfill_count", "his":"m:", "kind":"s:Number", "lastHisTime":"t:2020-04-28T09:40:00Z", "lastHisVal":"n:0", "name":"s:backfill_count", "point":"m:", "siteRef":"r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub \\\"Test Site\\\"", "tz":"s:UTC", "wsgServiceConfig":"s:type: backfill_count\n", "wshPoint":"n:10"},
{"id":"r:6d320af3-c392-4fd5-875f-289ce16f4b9b backfill_lag", "dis":"s:backfill_lag", "equipRef":"r:be4cc43c-86d8-4167-9642-07d8f8ea3475 Hub #9 (7b54)", "fqname":"s:ws.hub7b54.backfill_lag", "his":"m:", "kind":"s:Number", "lastHisTime":"t:2020-04-28T07:38:00Z", "lastHisVal":"n:120", "name":"s:backfill_lag", "point":"m:", "siteRef":"r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub \\\"Test Site\\\"", "tz":"s:UTC", "wsgServiceConfig":"s:type: backfill_lag\n", "wshPoint":"n:4"}
]}
```
