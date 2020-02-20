---
title: "Configuration"
linkTitle: "Configuration"
weight: 2
type: docs
description: >
  Configuring Grafana to use WideSky.
---
## Configuring the data source
Grafana requires a data source to be configured. To configure the WideSky data source:
1. Open the side menu by clicking the Grafana icon in the top header.
2. In the side menu under the Dashboards link you should find a link named Data Sources.
3. Click the + Add data source button in the top header.
4. Select WideSky from the type drop down menu.
5. Complete the fields in the following table.

{{% alert title="Note"  color="info" %}} If you’re not seeing the Data Sources link in your side menu it means that your current user does not have the Admin role for the current Grafana organization.
{{% /alert %}}

|Name|Description|
|------|-----------|
|*Name*|The data source name. This is how you refer to the data source in panels and queries|
|*Default*|Default data source means that it will be pre-selected for new panels|
|*URL*|The URL of your WideSky e.g. https://lab.on.widesky.cloud/widesky |
|*Access*|Server *(recommended)* or Browser|
|*Client id*|Your WideSky account Client id|
|*Client Secret*|Your WideSky account Client Secret|
|*Username*|The name of your WideSky user|
|*Password*|WideSky user’s password|


### Access Mode

Access mode controls how requests to the data source will be handled.

### Server access mode (Default)

All requests will be made from the browser to Grafana back-end/server which in turn will forward the requests to the data source and by that circumvent possible Cross-Origin Resource Sharing (CORS) requirements.

### Browser access mode
All requests will be made from the browser directly to the data source and may be subject to Cross-Origin Resource Sharing (CORS) requirements. The URL needs to be accessible from the browser if you select this access mode.

