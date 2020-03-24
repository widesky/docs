---
title: "Visualisation"
linkTitle: "Visualisation"
weight: 3
type: docs
description: >
  Build asset-based analytics and generate data insights
---

## Overview
The [WideSky Cloud](https://widesky.cloud/products/widesky-cloud) analytics and visualization tool is based on the open-source [Grafana](https://www.grafana.com) platform. This tool provides analytics, dashboards, charts and graphs and allows and end-users to create sophisticated monitoring dashboards and templates using an interactive query builder.

Using this tool, you can:
+ Empower end-users with self-service analytics
+ Create sophisticated monitoring dashboards and templates
+ Perform real-time supervisory control of devices
+ Securely service multiple end-customers via a single WideSky Cloud instance
+ Share data insights and knowledge via the web or mobile devices
+ View and administer all of the  time-series data and asset models


## WideSky data plugin for Grafana

We've extended Grafana to included a feature-rich data plugin for WideSky using the [GraphQL API](../../../reference/apis/cloud/graphql/). This plug-in includes a variety of features to assist with the analytics construction, including:
+ An interactive query builder that supports:
  + Contextually aware Project Haystack filter suggestions
  + GraphQL schema introspection and helper text to provide contextually aware choices
+ Support for both time series and table panel types
+ Support for Grafana templates
+ Real-time control buttons

You will be issued with a URI and administrator level credentials. You can use the guides below to understand how to user the plugin.

{{% alert title="Note"  color="primary" %}} If you're new to Grafana, we recommend visiting their [getting started guide](https://grafana.com/docs/grafana/latest/guides/getting_started/) to get acquainted with Grafana basics.
{{% /alert %}}
