---
title: "widesky-editor YAML"
weight: 2
type: docs
description: >
  "YAML" Ain't a Markup Language format reference
---
`widesky-editor`'s full power is realised when the [YAML](https://yaml.org/) file format is used. It supports all Project Haystack data types and allows you to edit multiple entities in a single action by using filters.

{{% alert title="Tip" %}}
For best compatibility, we recommend using [YAML 1.0](https://yaml.org/spec/1.0/)
{{% /alert %}}

The format used by `widesky-editor` exploits YAML's ability to handle multiple "documents" within a single file, separating each document with a document separator: `---`.  Each "document" within the file encodes a single "action" for the editor to execute. Project Haystack's [JSON](https://project-haystack.org/doc/Json) format is used to represent tag values.


## Actions

{{% alert title="Warning"   color="warning" %}}
The actions are executed in the order encountered. It is of utmost importance that referential integrity is maintained when issuing instructions.
{{% /alert %}}

All documents encoding an action to be performed must be written as a YAML map object:

```
---
action: ${ACTION}
# Other parameters go here
---
```

Below is a summary of available actions:

|Action|Description|
|------|----|-----------|
|`create`|Create a new entity|
|`create_or_update`|See if a given entity exists, and either update its tags, or if the entity is not present, create it with the tags given.|
|`create_or_set`|See if a given entity exists, and either set the tags given tags, or if the entity is not present, create it with the tags given.|
|`delete`|deletes entities, either by ID or by filter|
|`update`|Update the tags of given entities|
|`set`|Update the tags of given entities, and remove any tags not explicitly listed.|


### create

Create will try to create a new entity with the given ID, failing if the entity already exists.

```
---
action: create
# ID for the entity.  Either a UUID or a fully-qualified name
id: ${UUID_OR_FQNAME}
tags:
    # Your new entity's tags, given in Haystack JSON format
    # e,g.
    dis: "s:A new site"
    site: "m:"		# Important! put quotes around markers!
---
```

### create_or_update

See if a given entity exists, and either update its tags, or if the entity is not present, create it with the tags given.

If the entity already exists, the tags listed will be changed to the values given, *leaving all other tags unchanged*.

As the name suggests, this does a [`create`](#create) if the entity is new, or an [`update`](#update) if it already exists.

```
---
action: create_or_update
# ID for the entity.  Either a UUID or a fully-qualified name
id: ${UUID_OR_FQNAME}
tags:
    # Your new entity's tags, given in Haystack JSON format
    # e,g.
    dis: "s:A new site"
    site: "m:"		# Important! put quotes around markers!
---
```

To delete tags from an entity, list them in `delete_tags`:

```
---
action: create_or_update
id: my.entity.point
tags: {}	# Not changing existing tags
delete_tags:
- energy	# Delete the 'energy' tag
```

### create_or_set

See if a given entity exists, and either set the tags given, or if the entity is not present, create it with the tags given.

{{% alert title="Warning"   color="warning" %}}
If the entity already exists, the tags listed will be changed to the values given, and any tag not listed will be deleted.
{{% /alert %}}

As the name suggests, this does a [`create`](#create) if the entity is new, or a [`set`](#set) if it already exists.

```
---
action: create_or_set
# ID for the entity.  Either a UUID or a fully-qualified name
id: ${UUID_OR_FQNAME}
tags:
    # Your new entity's tags, given in Haystack JSON format
    # e,g.
    dis: "s:A new site"
    site: "m:"		# Important! put quotes around markers!
---
```

To delete tags from an entity, list them in `delete_tags`:

```
---
action: create_or_set
id: my.entity.point
tags: {}	# Not changing existing tags
delete_tags:
- energy	# Delete the 'energy' tag
```

### delete

This deletes entities, either by ID or by filter.  Both can be specified simultaneously in an action, the order of processing will be:

1. The entity listed by the argument, `id`
2. Entities listed by the argument, `ids` in the order given
3. All entities returned by a search performed with the filter expression given in the `filter` argument.  Ordering is not guaranteed.
4. All entities returned by a search performed with each filter expression given in the `filters` argument (searched in that order).  Ordering is not guaranteed.

#### Delete one entity by ID

To delete a single point, give its ID as the `id` parameter:
```
---
action: delete
id: my.unwanted.point
---
```

#### Delete many entities by ID

For quick deletion of multiple entities, list them as `ids`:
```
---
action: delete
ids:
- my.unwanted.point2
- e3f59ec1-8876-49e2-9d4f-635c738ac2a1
---
```

#### Delete many entities by filter

A [Project Haystack filter](https://project-haystack.org/doc/Filters) string can be used to delete entities.

```
---
action: delete
# The filter string must be given in the Project Haystack filter syntax
# which is based on their ZINC encoding scheme.
filter: point and equipRef==@my.unwanted and energy
---
```

You can also specify multiple filters with the `filters` argument:
```
---
action: delete
filters:
- point and siteRef==@oldSite
- equip and siteRef==@oldSite
---
```

### update

Update the tags of given entities.  The entities to update can either be explicitly listed, or we can do a search for those matching a given filter.

All tags listed in the `tags` argument will be updated to the given values.  Tags _not_ listed will be left unchanged.

Like the `delete` instruction above, the entities are chosen and updated in the following order:

1. The entity listed by the argument, `id`
2. Entities listed by the argument, `ids` in the order given
3. All entities returned by a search performed with the filter expression given in the `filter` argument.  Ordering is not guaranteed.
4. All entities returned by a search performed with each filter expression given in the `filters` argument (searched in that order).  Ordering is not guaranteed.

Tags can be deleted by listing them in `delete_tags`.

#### Update one entity by ID

```
---
action: update
id: ${FQN_OR_UUID}
tags:
  # New tag values, e.g.
  dis: "s:New description"
---
```

Or to delete tags from that entity:

```
---
action: update
id: ${FQN_OR_UUID}
tags: {} # No tag changes
delete_tags:
- myUnwantedTag
---
```

#### Update many by ID

```
---
action: update
ids:
- ${FQN_OR_UUID1}
- ${FQN_OR_UUID2}
- ${FQN_OR_UUID3}
tags:
  # New tag values, e.g.
  dis: "s:New description"
---
```

Or to delete tags from that entity:

```
---
action: update
ids:
- ${FQN_OR_UUID1}
- ${FQN_OR_UUID2}
- ${FQN_OR_UUID3}
tags: {} # No tag changes
delete_tags:
- myUnwantedTag
---
```

#### Update many by filter

A single [filter](https://project-haystack.org/doc/Filters):

```
---
action: update
filter: point and energy
tags:
  unit: "s:kWh"
  kind: "s:Number"
---
```

Or multiple filters:
```
---
action: update
filters:
- point and energy
- point and freq
- point and power
tags:
  kind: "s:Number"
---
```

### set

Update the tags of given entities, and remove any tags not explicitly listed.  The entities to update can either be explicitly listed, or we can do a search for those matching a given filter.

{{% alert title="Warning"   color="warning" %}}
All tags listed in the `tags` argument will be updated to the given values.  Tags _not_ listed will be **deleted**.
{{% /alert %}}

Like the `delete` instruction above, the entities are chosen and updated in the following order:

1. The entity listed by the argument, `id`
2. Entities listed by the argument, `ids` in the order given
3. All entities returned by a search performed with the filter expression given in the `filter` argument.  Ordering is not guaranteed.
4. All entities returned by a search performed with each filter expression given in the `filters` argument (searched in that order).  Ordering is not guaranteed.

Tags can be deleted by listing them in `delete_tags`.

#### Set one entity by ID

```
---
action: set
id: ${FQN_OR_UUID}
tags:
  # New tag values, e.g.
  dis: "s:New description"
---
```

Or to delete tags from that entity:

```
---
action: set
id: ${FQN_OR_UUID}
tags: {} # No tag changes
delete_tags:
- myUnwantedTag
---
```

#### Set many by ID

```
---
action: set
ids:
- ${FQN_OR_UUID1}
- ${FQN_OR_UUID2}
- ${FQN_OR_UUID3}
tags:
  # New tag values, e.g.
  dis: "s:New description"
---
```

Or to delete tags from that entity:

```
---
action: set
ids:
- ${FQN_OR_UUID1}
- ${FQN_OR_UUID2}
- ${FQN_OR_UUID3}
tags: {} # No tag changes
delete_tags:
- myUnwantedTag
---
```

#### Set many by filter

A single [filter](https://project-haystack.org/doc/Filters):

```
---
action: set
filter: point and energy
tags:
  unit: "s:kWh"
  kind: "s:Number"
---
```

Or multiple filters:
```
---
action: set
filters:
- point and energy
- point and freq
- point and power
tags:
  kind: "s:Number"
---
```

## Examples

### Creating a site, spaces, equipment and points

```
action: create_or_set
id: ws
tags:
  dis: s:WideSky Hub "Test Site"
  site: 'm:'
---
action: create_or_set
id: ws.rack1l
tags:
  dis: s:Test Rack Row 1 Left
  siteRef: r:ws
  space: 'm:'
---
action: create_or_set
id: ws.wshub281hub6
tags:
  device: 'm:'
  dis: s:Hub 00124b0018e423cc
  equip: 'm:'
  siteRef: r:ws
  spaceRef: r:ws.rack1l
  tz: s:GMT-10
  wsgHistoricalInterval: n:120.000000
  wsgHistoricalOffset: n:24.000000
  wsgServiceConfig: |-
    update:
          config_int: 60
          firmware_int: 60
          block_sz: 256
    console:
          baud: 115200
          parity: N
          bytesize: 8
          stopbits: 1
          timeout_mode: console
          flow_control: none
          parity_err: discard
          rx_port: 2
          tx_port: 1
    syslog:
          level: 3
          persist: 0
  wshEui64: s:00124b0018e423cc
  wshFirmwareVer: s:1.3.4-alpha.26+200320T0732-ce075f89
  wshRTLifetime: n:300.000000
  wshRTTimeout: n:60.000000
  wshToEnrol: 'm:'
---
action: create_or_set
id: ws.wshub281hub6.parent_rssi
tags:
  dis: s:parent_rssi
  equipRef: r:ws.wshub281hub6
  his: 'm:'
  kind: s:Number
  point: 'm:'
  siteRef: r:ws
  tz: s:UTC
  wsgServiceConfig: |
    type: parent_rssi
---
action: create_or_set
id: ws.wshub281hub6.backfill_count
tags:
  dis: s:backfill_count
  equipRef: r:ws.wshub281hub6
  his: 'm:'
  kind: s:Number
  point: 'm:'
  siteRef: r:ws
  tz: s:UTC
  wsgServiceConfig: |
    type: backfill_count
---
action: create_or_set
id: ws.wshub281hub6.hgm_state
tags:
  dis: s:hgm_state
  equipRef: r:ws.wshub281hub6
  his: 'm:'
  kind: s:Number
  point: 'm:'
  siteRef: r:ws
  tz: s:UTC
  wsgServiceConfig: |
    type: hgm_state
```

### Changing a tag on an entity who's ID is unknown

Here, we don't know the ID, but we know some other attribute for that entity which happens to also be unique:

```
action: update
filter: wshEui64=="00124b0011f47b54"
tags:
  wshFirmwareVer: s:1.3.4-alpha.11
```
