---
title: "Using Editor"
linkTitle: "Using Editor"
weight: 3
type: docs
draft: true
description: >
  How to use WideSky Editor.
---

See the Getting Started guide for basic operation.

## Commands
WideSky editor has 2 sub-commands.

### Dump
Dumps entity information from WideSky.

You can specify an explicit entity `id` to dump or speficy a [Project Haystack filter](https://project-haystack.org/doc/Filters) to dump matching entities.


### Load
Load entity changes into the server


## File Formats

You can use either CSV or YAML file formats.

### CSV

### YAML

A WideSky editor yaml file looks like this:
```yaml
---
action: create_or_set
id: 0f9bb59c-9a78-48c8-a2d8-64c28bd5b26a
tags:
  device: 'm:'
  dis: s:Energy Meter
  elec: 'm:'
  equip: 'm:'
  fqname: s:ws.0f9bb59c-9a78-48c8-a2d8-64c28bd5b26a
  modbusUnitId: n:50.000000
  name: s:0f9bb59c-9a78-48c8-a2d8-64c28bd5b26a
  siteRef: r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub Test Site
  spaceRef: r:8385e7f7-1d80-4673-bb88-bcd69a610f01 rack1r
---
action: create_or_set
id: 1041fc70-40de-40da-801f-5fd7e12bb580
tags:
  device: 'm:'
  dis: s:Energy Meter
  elec: 'm:'
  equip: 'm:'
  fqname: s:ws.1041fc70-40de-40da-801f-5fd7e12bb580
  modbusUnitId: n:45.000000
  name: s:1041fc70-40de-40da-801f-5fd7e12bb580
  siteRef: r:70624619-de61-4f6c-aaf7-014443123f39 WideSky Hub Test Site
  spaceRef: r:2f42768a-5b45-4002-8072-472079e0787a rack2l
```

#### YAML Commnads

A YAML file can contain one or more documents, each document is considered a command for WideSky Editor.

Each command can have the following:

|Name|Description|
|------|-----------|
|\-\-\-|yaml document start indicator|
|*action*|The action to take|
|(Optional) *tags*|A block of tags to be assigned, edited or deleted|
|(Optional) *filter* OR *id*| A [Project Haystack filter](https://project-haystack.org/doc/Filters) or entity id|

{{% alert title="Tip"  color="primary" %}}
The id can ether be a UUID or Fully-Qualified Name.
{{% /alert %}}


List of action types:

|Action|Description|
|------|-----------|
|*create*|Create a new entity|
|*delete*|Delete the entity or entities|
|*set*|Set the tags are explicitly listed in the command. Tags that are not listed are removed|
|*update*|Update tags that are listed in the command|
|*create_or_update*|Update the entitiy with the tags, if it does not exist create it|
|*create_or_set*|Set the tags are explicitly listed in the command. Tags that are not listed are removed. If the entitiy does not exist, create it|


#### Examples:


##### Delete
```
action: delete
id: ce1e2a7e-4afc-11ea-85d5-0242ac120003
```

##### create_or_update

Generic id

Specifying name


Explicit id
```
---
action: create_or_update
id: ea99fab6-4afc-11ea-a891-0242ac120003
tags:
  dis: s:A Test point
  equipRef: r:ce344476-4afc-11ea-85d6-0242ac120003 A Test equip made by editor
  name: s:editorTestPoint
  point: 'm:'
  siteRef: r:ce1e2a7e-4afc-11ea-85d5-0242ac120003 A Test site made by editor
```
A new site entitiy will be created each time this command is run


##### update


By Filter:
Add the `wshToEnrol` tag to all entities that have `wshEui64`
```
action: update
filter: wshEui64
tags:
        wshToEnrol: 'm:'
```


## Read-Only tags
The following tags are read-only in WideSky and are ignored by WideSky editor:
+`curVal`
+`curStatus`
+`curErr`
+`fqname`
