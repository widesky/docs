---
title: "WideSky Edge"
weight: 200
type: docs
description: >
  WideSky Edge documentation.
---

# Overview
WideSky Edge is a suite of software for creating reliable operational data solutions. With a seamless interface to WideSky Cloud, it delivers three critical benefits to your business:

- Translate and Interpret multiple devices that talk multiple languages throughout your enterprise into a single system.
- Allow 24 x 7 data continuity even for extended offline periods.
- Distributed architecture that moves intelligence closer to the data source allowing for increased reliability.

## Flow programming
Based on the open source project [Node-RED](https://nodered.org/), you can easily create robust IoT solutions in a friendly browser-based flow editor. We have built WideSky specific [nodes](./nodes/) for protocol conversion, data capture, analytics and more.

## Distributed WideSky Architecture
The WideSky Edge architecture was designed to ensure your IoT solutions are reliable, efficient and continue to operate during extended offline periods. You can distribute WideSky data processing workloads and time series data capture. To ensure data reliability and local processing can continue in the event of extended communications outages, it:

- Stores time series data localy and backfills to WideSky Cloud when communications is reestablished to avoid data loss
- Serves time series and asset model data via a local GraphQL API for local data processing workflows

## Easy deployment
### Docker
We've packaged WideSky Edge in a single docker container for both x86 and raspberry pi architectures for a simple deployment.

### IoTium
You can also use WideSky Edge in the IoTium app store. IoTium provides a secure managed software-defined network infrastructure for industrial IoT.
