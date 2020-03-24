---
title: "Getting Started"
linkTitle: "Getting Started"
weight: 2
type: docs
description: >
  How to get started with WideSky Editor.
---

Learn how how to create, read, update & delete entities using the CSV mode.

### Prerequisites

Make sure you have already installed [WideSky Editor](../installation/). You will also need your WideSky Cloud credentials.


## Create, Read, Update & Delete entities
### Step 1: Setup

Create a directory for the project:
```bash
$ mkdir editortest
$ cd editortest
```

### Step 2: Create a CSV file containing new entity definitions

Using a text editor, write the following contents into a new CSV file named `testModel.csv`:
```csv
id,delete,dis,site,equip,point,siteRef,equipRef,name
,,s:A test site made by editor,m:,,,,,s:editorTestSite
,,s:A test equip,,m:,,r:editorTestSite,,s:editorTestEquip
,,s:A test point,,,m:,r:editorTestSite,r:editorTestSite.editorTestEquip,s:editorTestPoint
```

### Step 3: Write the new entities to WideSky

Use the `load` command and specify `--csv-in` to load in the new CSV file and create the entities in WideSky.

```bash
$ widesky-editor \
        --uri <URI> \
        --user <USERNAME> \
        --password "<PASSWORD>" \
        --client-id "<CLIENT_ID>" \
        --client-secret "<CLIENT_SECRET>" \
    load --csv-in testModel.csv
```

You should see output similar to the following:

```bash
INFO:root:Read from <open file 'test2.csv', mode 'r' at 0x7f43485fa390>
INFO:root:Action create Changed: ce1e2a7e-4afc-11ea-85d5-0242ac120003
INFO:root:Action create Changed: ce344476-4afc-11ea-85d6-0242ac120003
INFO:root:Action create Changed: ea99fab6-4afc-11ea-a891-0242ac120003
```

### Step 4: Read the newly created entities

Use the `dump` command and use the `--filter` argument to specify the entities we're after.

```bash
$ widesky-editor --output testEntities.csv \
        --csv \
        --uri <URI> \
        --user <USERNAME> \
        --password "<PASSWORD>" \
        --client-id "<CLIENT_ID>" \
        --client-secret "<CLIENT_SECRET>" \
    dump \
        --filter 'siteRef==@editorTestSite or id==@editorTestSite'
```
You should see the following response:

```bash
INFO:root:Searching: 'siteRef==@editorTestSite or id==@editorTestSite'
INFO:root:Found 3
```
The file test entities should contain similar contents. Notice that WideSky has created UUIDs for each entity.

![Test entities](/docs/images/editor-test-entities.png)


### Step 5: Edit an entity

Add a new tag `geoCity` to the `site` entity.

1. In your spreadsheet application or text editor, insert a new column with the heading `geoCity`.
2. Add a city name e.g. `s:Brisbane` to the row with the `site` entity, and save the CSV file.
  ![Add geoAddr to the site entity](/docs/images/editor-add-geoAddr.png)
3. Use WideSky Editor to read the file and update each entity:

```bash
$ widesky-editor \
        --uri <URI> \
        --user <USERNAME> \
        --password "<PASSWORD>" \
        --client-id "<CLIENT_ID>" \
        --client-secret "<CLIENT_SECRET>" \
    load --csv-in testEntities.csv
```
    You should see the following response:
```bash
INFO:root:Read from <open file 'dump.csv', mode 'r' at 0x7f848f2bc390>
WARNING:root:fqname is a read-only tag, ignoring
INFO:root:For ce344476-4afc-11ea-85d6-0242ac120003: setting {}, deleting set([])
INFO:root:Action update Changed: ce344476-4afc-11ea-85d6-0242ac120003
WARNING:root:fqname is a read-only tag, ignoring
INFO:root:For ea99fab6-4afc-11ea-a891-0242ac120003: setting {}, deleting set([])
INFO:root:Action update Changed: ea99fab6-4afc-11ea-a891-0242ac120003
WARNING:root:fqname is a read-only tag, ignoring
INFO:root:For ce1e2a7e-4afc-11ea-85d5-0242ac120003: setting {'geoAddr': u'Brisbane'}, deleting set([])
INFO:root:Action update Changed: ce1e2a7e-4afc-11ea-85d5-0242ac120003
action: create_or_update
changed:
- ce344476-4afc-11ea-85d6-0242ac120003
id: ce344476-4afc-11ea-85d6-0242ac120003
tags:
  dis: s:A Test equip made by editor
  equip: 'm:'
  fqname: s:editorTestSite.editorTestEquip
  name: s:editorTestEquip
  siteRef: r:ce1e2a7e-4afc-11ea-85d5-0242ac120003 A Test site made by editor
---
action: create_or_update
changed:
- ea99fab6-4afc-11ea-a891-0242ac120003
id: ea99fab6-4afc-11ea-a891-0242ac120003
tags:
  dis: s:A Test point made by editor
  equipRef: r:ce344476-4afc-11ea-85d6-0242ac120003 A Test equip made by editor
  fqname: s:editorTestSite.editorTestEquip.editorTestPoint
  name: s:editorTestPoint
  point: 'm:'
  siteRef: r:ce1e2a7e-4afc-11ea-85d5-0242ac120003 A Test site made by editor
---
action: create_or_update
changed:
- ce1e2a7e-4afc-11ea-85d5-0242ac120003
id: ce1e2a7e-4afc-11ea-85d5-0242ac120003
tags:
  dis: s:A Test site made by editor
  fqname: s:editorTestSite
  geoAddr: s:Brisbane
  name: s:editorTestSite
  site: 'm:'
```

### Step 6: Delete the entities

1. To delete the entities add `m:` to all three entities:

   ![Add m: in the delete column to delete entities](/docs/images/editor-delete-entities.png)

2. Load the file again with the command:

```bash
$ widesky-editor \
        --uri <URI> \
        --user <USERNAME> \
        --password "<PASSWORD>" \
        --client-id "<CLIENT_ID>" \
        --client-secret "<CLIENT_SECRET>" \
    load --csv-in testEntities.csv
```
You should see the following response:

```bash
INFO:root:Read from <open file 'dump.csv', mode 'r' at 0x7fedfebfc390>
INFO:root:Deleting IDs: ce344476-4afc-11ea-85d6-0242ac120003
...
```

## Where to go next
+ Understand the YAML mode that provides more powerful commands
