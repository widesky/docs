---
title: "REST"
linkTitle: "REST"
weight: 2
Description: The API for editing and controlling entities, and reading / writing time series data. Based on Project Haystack API specification.
type: docs
---

## Overview
The WideSky Cloud REST API exposes a range of functionality to query the asset model, read and write data, and issue commands. It's based on the REST architectural style, and in particular implements a superset of the  <a href="https://project-haystack.org/doc/Rest" target="_blank" rel="noopener">Project Haystack REST API Specification</a>.

{{% alert title="Note"  color="primary" %}} Technically the Haystack REST API isn't strictly "RESTful" from a purist perspective - the ops design is more akin to a RPC model. But we use the term REST to distinguish the design from traditional WS-\* web services that use XML, SOAP, etc.
{{% /alert %}}

## Operations
A haystack REST server implements a set of operations (or "ops"). Standard operations are defined to query WideSky, setup subscriptions, or read/write history time series data. Both requests and responses are modelled as grids. Grids are encoded using either ZINC or JSON serialization formats.

### Serialization
All data is exchanged in Project Haystck [grids](./serialization) in either ZINC or JSON format.

### Ops Summary

A summary of the currently support operations is listed below:

|Method|URI|Haystack Standard|WideSky Support|Description|
|------|---|-----------------|---------------|-----------|
|About|`/api/about`|✓|✓|The `about` op queries basic information about the server.|
|Operations|`/api/ops`|✓|✓|The `ops` op queries which operations are available on the server.|
|Formats|`api/formats`|✓|✓|The `formats` op is used to query which MIME types are available to read and write grids.|
|Create|`/api/createRec`|☓|✓|The `createRec` op is used to create new entity records in the asset model.|
|Read|`/api/read`|✓|✓|The `read` op is used to read a set of entity records either by their unique identifier or using a filter.|
|Update|`/api/updateRec`|☓|✓|The `updateRec` op is used to add, update or delete the tags on a entity records.|
|Delete|`/api/deleteRec`|☓|✓|The `deleteRec` op is used for deleting entity records either by their unique identifier or using a filter.|
|Navigate|`/api/nav`|✓|☓|The `nav` op is used navigate a project for learning and discovery. Allowing servers to expose the database in a human-friendly tree (or graph).|
|Watch Subscribe|`/api/watchSub`|✓|✓|The `watchSub` operation is used to create new watches or add entities to an existing watch.|
|Watch Unsubscribe|`/api/watchUnsub`|✓|✓|The `watchUnsub` operation is used to close a watch entirely or remove entities from a watch.|
|Watch Poll|`/api/watchPoll`|✓|✓|The `watchPoll` operation is used to poll a watch for changes to the subscribed entity records.|
|Point Write|`/api/pointWrite`|✓|✓*|The `pointWrite` op is used to read the current status of a writable point's priority array and optionally write to a given level.|
|Historical Write|`/api/hisWrite`|✓|✓*|The `hisWrite` op is used to post new time series data to a historised point.|
|Historical Read|`/api/hisRead`|✓|✓*|The `hisRead` op is used to read time series data from historised point.|
|Invoke Action|`/api/invokeAction`|✓|☓|The `invokeAction` op is used to invoke an user action on a target entity.|
|Update Password|`/api/updatePassword`|✓|☓|The `updatePassword` op is used for changing a Widesky user’s password.|

\* Indicates standard operation is supported with added functionality.
