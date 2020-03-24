---
title: "Configuration"
linkTitle: "Configuration"
weight: 2
type: docs
description: >
  Configuring the WideSky data source.
---
## Configuring the data source
Grafana requires a configured data source before building dashboards. To configure the WideSky data source:
1. Open the side menu by clicking the Grafana icon in the top header.
2. In the side menu under the _Dashboards_ link you should find a link named _Data Sources_.
3. Click the _+ Add data source_ button in the top header.
4. Select _WideSky_ from the _Type_ drop-down menu.
5. Complete the fields in the following table.

{{% alert title="Note"  color="info" %}} If you do not see the _Data Sources_ link in your side menu it means that your current user does not have the _Admin_ role for the current Grafana organization.
{{% /alert %}}

|Name|Description|
|------|-----------|
|*Name*|The data source name|
|*Default*|Default data source means that it is pre-selected for new panels|
|*URL*|The URL of your WideSky, e.g. https://lab.on.widesky.cloud/widesky |
|*Access*|Server *(recommended)* or Browser|
|*Client id*|Your WideSky account Client id|
|*Client Secret*|Your WideSky account Client Secret|
|*Username*|The name of your WideSky user|
|*Password*|WideSky user’s password|


### Access Mode

Access mode controls how requests to the data source are handled by the browser.

### Server access mode (Default)

All requests are made from the browser to Grafana backend/server which in turn forwards the requests to the data source and by that circumvent possible Cross-Origin Resource Sharing (CORS) requirements.

### Browser access mode
All requests are made from the browser directly to the data source and may be subject to Cross-Origin Resource Sharing (CORS) requirements. The URL needs to be accessible from the browser if you select this access mode.
