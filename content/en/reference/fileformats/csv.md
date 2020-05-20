---
title: "widesky-editor CSV"
weight: 1
type: docs
description: >
  Comma-Separated Values format reference
---

`widesky-editor` supports a simplified CSV format for use with spreadsheeting applications.  The schema is deliberately limited in its scope to maximise compatibility with spreadsheet tools.

## File format

### Row 1: Header row

The first row is *always* used for header information:

|Cell Position|Description|
|-------------|-----------|
|A1|Labels the column storing ID references, content is ignored|
|B1|Labels the column storing the "delete" flag, content is ignored|
|C1-ZZ1|Name of the tag allocated to this column|

### Row 2 onwards: Data rows

For all subsequent rows:

|Column|Description|
|------|-----------|
|A|ID of the entity being created/updated/deleted.  This is _assumed_ to be either the fully qualified name or the UUID of the entity.|
|B|Delete flag.  If any text is written to this cell, the entity referenced by this row will be deleted when the file is loaded by `widesky-editor`.|
|C-ZZ|Values for the tags listed in the first row.  If the cell is left blank, the corresponding tag is left unchanged on the entity.  The values themselves are encoded using [JSON](https://project-haystack.org/doc/Json) format.|

#### Encoding tag values

All tag values are encoded using the Project Haystack JSON format. Below are the supported data types:

* **Text strings** should be prefixed by `s:`.
  * `s:My string`
* **Numbers** should be prefixed by `n:`, and if a unit of measure is to be included, that can be put at the end separated by a space.
  * `n:1234` (without unit)
  * `n:1234 kWh` (with unit)
* **References** (in UUID or fully qualified name form) must be prefixed by `r:` and can optionally include a descriptive name separated by a space.
  * `r:my.ref` (fully qualified name without descriptive text)
  * `r:my.ref My entity` (fully qualified name with descriptive text)
  * `r:d19a3670-6868-441a-8d6c-f461ea6d10ca` (UUID without descriptive text)
  * `r:d19a3670-6868-441a-8d6c-f461ea6d10ca My entity` (UUID with descriptive text)
* Tags are **removed** by writing `x:` as the value (this is the older Project Haystack 2.0 syntax which predates the newer `-:` syntax)
* **Dates** are written in ISO-8601 format with a `d:` prefix
  * `d:2020-03-26`
* **Times** are written in IS0-8601 format with a `h:` prefix
  * `h:13:29:24`
* **Date/Time timestamps** are written in ISO-8601 format with a `t:` prefix and the time zone name suffixed with a space.
  * `t:2020-03-26T13:29:24 Brisbane`

{{% alert title="Tip" %}}
Use the [YAML](../yaml/) file format for support of other Project Haystack data types.
{{% /alert %}}

### Handling of special characters

In CSV, values are separated by commas (`,`).  In situations where a comma appears *inside* a value, the entire value must be enclosed in double quotes (`"`).

Where a value that is to be "enclosed" in double quotes itself contains double quotes, each instance of the double quote shall be "doubled".

* `A string, with a comma` should be written out as `"A string, with a comma"`.
* `A string, with a comma and "quotes" within` should be written out as `"A string, with a comma and ""quotes"" within"`.

Most spreadsheeting tools will automatically handle this for you.

## Examples

### Creating or updating sites, equips and points

Entities need to be created in dependency-order, that is, `site` entities must be created before `equip` and `point` entities (because their `siteRef` tags reference them) and `equip` entities must be created before `point` entities (because their `equipRef` tags reference them).

The "name" of each entity is taken from the `ID` column: the ID is split on the dots (`.`) and the _last_ part taken.

|`ID`|`Delete`|`dis`|`site`|`siteRef`|`equip`|`equipRef`|`point`|
|----|--------|-----|------|---------|-------|----------|-------|
|`mySite`||`s:A new WideSky site`|`m:`|||||
|`mySite.myEquip`||`s:A piece of equipment in the site`||`r:mySite`|`m:`|||
|`mySite.myEquip.myPoint`||`s:A point on the equipment`||`r:mySite`||`r:mySite.myEquip`|`m:`|

```text
"ID","Delete","dis","site","siteRef","equip","equipRef","point"
"mySite","","s:A new WideSky site","m:","","","",""
"mySite.myEquip","","s:A piece of equipment in the site","","r:mySite","m:","",""
"mySite.myEquip.myPoint","","s:A point on the equipment","","r:mySite","","r:mySite.myEquip","m:"
```

### Deleting entities

Deleting entities requires that we maintain referential integrity by deleting all references to an entity before we delete the entity itself.  Therefore, `point` entities should be deleted first, then `equip`s, then `site`s.

When performing a delete, all columns C-ZZ are ignored.  They can be present to help the user recognise which entities are being marked for deletion, but in this mode their values are not critical.  (Typically in this use case, the user is editing a spreadsheet produced by the `widesky-editor dump` command.)

_Any_ non-empty text value in column B (including `no` or `false`) is treated as a "delete" request.  To _not_ delete an entity, _leave the cell blank!_

|`ID`|`Delete`|`dis`|`site`|`siteRef`|`equip`|`equipRef`|`point`|
|----|--------|-----|------|---------|-------|----------|-------|
|`mySite.myEquip.myPoint`|`X`|`s:A point on the equipment`||`r:mySite`||`r:mySite.myEquip`|`m:`|
|`mySite.myEquip`|`X`|`s:A piece of equipment in the site`||`r:mySite`|`m:`|||
|`mySite`|`X`|`s:A new WideSky site`|`m:`|||||

```text
"ID","Delete","dis","site","siteRef","equip","equipRef","point"
"mySite.myEquip.myPoint","X","s:A point on the equipment","","r:mySite","","r:mySite.myEquip","m:"
"mySite.myEquip","X","s:A piece of equipment in the site","","r:mySite","m:","",""
"mySite","X","s:A new WideSky site","m:","","","",""
```

### Mixing operations

It is entirely valid to mix entity creation, updates and deletions within the one spreadsheet.  The rows are "executed" from row 2 onwards in the order given.  The only requirement is that referential integrity is maintained (you cannot reference an entity that does not yet exist, nor can you delete an entity that is still being referenced).

In this example, we delete two entities (which were dumped by `widesky-editor`), then update some other entities and add some new points.  We also use UUIDs to reference the existing entities (to show it can be done).

|`ID`|`Delete`|`dis`|`site`|`siteRef`|`equip`|`equipRef`|`point`|
|----|--------|-----|------|---------|-------|----------|-------|
|`c5ca843c-d294-4fd9-88ff-e839192aff15`|`X`|`s:kWh Import`||`r:2e78589c-a34d-4907-8d95-ee362bc7d56d Milton Office`||`r:44ea0813-43d9-460f-a700-591ff59dc31e Server Room Meter #1`|`m:`|
|`44ea0813-43d9-460f-a700-591ff59dc31e`|`X`|`s:Server Room Meter #1`||`r:2e78589c-a34d-4907-8d95-ee362bc7d56d Milton Office`|`m:`|||
|`9b37384d-27b8-48f3-a2d7-487f6f03a516`||`s:Server Room Meter`||`r:2e78589c-a34d-4907-8d95-ee362bc7d56d Milton Office`|`m:`|||
|`wssyd`||`s:"Sydney Office"`|`m:`|||||
|`wssyd.incomer`||`s:"Main Incomer"`||`r:wssyd`|`m:`|||
|`wssyd.incomer.kwhImport`||`s:"kWh import"`||`r:wssyd`||`r:wssyd.incomer`|`m:`|

```text
"ID","Delete","dis","site","siteRef","equip","equipRef","point"
"c5ca843c-d294-4fd9-88ff-e839192aff15","X","s:kWh Import","","r:2e78589c-a34d-4907-8d95-ee362bc7d56d Milton Office","","r:44ea0813-43d9-460f-a700-591ff59dc31e Server Room Meter #1","m:"
"44ea0813-43d9-460f-a700-591ff59dc31e","X","s:Server Room Meter #1","","r:2e78589c-a34d-4907-8d95-ee362bc7d56d Milton Office","m:","",""
"9b37384d-27b8-48f3-a2d7-487f6f03a516","","s:Server Room Meter","","r:2e78589c-a34d-4907-8d95-ee362bc7d56d Milton Office","m:","",""
"syd","","s:"Sydney Office"","m:","","","",""
"wssyd.incomer","","s:"Main Incomer"","","r:wssyd","m:","",""
"wssyd.incomer.kwhImport","","s:"kWh import"","","r:wssyd","","r:wssyd.incomer","m:"
```
