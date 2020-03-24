---
title: "Schema reference"
linkTitle: "Schema reference"
weight: 3
type: docs
description: >
    The GraphQL schema reference documentation.
---

{{% alert title="Tip"  color="primary" %}}
The [visualisation tool](../interactive-graph) may provide a better experience for understanding the GraphQL documentation.
{{% /alert %}}

## `Query`
Query data from WideSky

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>haystack</strong></code></td>
<td valign="top"><a href="#haystack"><code>Haystack</code></a></td>
<td>

Query the semantic/historical data from WideSky

</td>
</tr>
</tbody>
</table>

## Objects

### `Bool`

Boolean "true" or "false".

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>bool</strong></code></td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td></td>
</tr>
</tbody>
</table>

### `Coord`

Geographic coordinate in latitude/longitude formatted as C(lat,lng)

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>coord</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

Geographic coordinate in latitude/longitude formatted as C(lat,lng) see https://project-haystack.org/doc/TagModel

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>geohash</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

A geographic location into a short string of letters and digits. see https://en.wikipedia.org/wiki/Geohash

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>longitude</strong></code></td>
<td valign="top"><a href="#float"><code>Float</code></a></td>
<td>

Measurement east or west of the prime meridian

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>latitude</strong></code></td>
<td valign="top"><a href="#float"><code>Float</code></a></td>
<td>

Measurement north or south of the Equator

</td>
</tr>
</tbody>
</table>

### `Date`

An ISO-8601 date as year, month, day: 2011-06-07

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>date</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td></td>
</tr>
</tbody>
</table>

### `DateTime`

A representation of date and time.

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>dateTime</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

A Project Haystack dateTime. Formatted as ISO-8601 timestamp followed by timezone name. e.g. 2011-06-07T09:51:27-04:00 New_York

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>isoDateTime</strong></code></td>
<td valign="top"><a href="#iso8601">iso8601</a></td>
<td>

ISO-8601 format

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>unixTime</strong></code></td>
<td valign="top"><a href="#unixtime"><code>UnixTime</code></a></td>
<td>

Unix timestamp in ms

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>timeZone</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

Haystack timezone see https://project-haystack.org/download/tz.txt

</td>
</tr>
</tbody>
</table>

### `Entities`

A collection of Entities -
        an abstraction for some physical objects in the real world.
        See https://project-haystack.org/doc/TagModel

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>history</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Retrieve the timeseries data from a list of entities.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">entityLimit</td>
<td valign="top"><a href="#int"><code>Int</code></a></td>
<td>

The maximum number of entities to return

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">rangeAbsolute</td>
<td valign="top"><a href="#absoluterange"><code>absoluteRange</code></a></td>
<td>

The absolute date time range of the history to retrieve

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">rangeRelative</td>
<td valign="top"><a href="#relativerange"><code>relativeRange</code></a></td>
<td>

The relative Time range of the history to retrieve

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>count</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

Return the number of entities in this set

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>entity</strong></code></td>
<td valign="top">[<a href="#entity"><code>Entity</code></a>]</td>
<td>

Perform more operations on the individual entity

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>search</strong></code></td>
<td valign="top"><a href="#entities"><code>Entities</code></a></td>
<td>

For each entity, search for more entities with a filter that also have a tag value {whereTag} that matches a tag value of the current entity {matchesTag} e.g. 'equipRef->id'

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">filter</td>
<td valign="top"><a href="#haystackfilter"><code>HaystackFilter</code></a>!</td>
<td>

A Project Haystack search filter e.g. equip and siteRef->geoCity == "Chicago" See https://project-haystack.org/doc/Filters

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">whereTag</td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Search for entities that reference the current entity by {whereTag}. e.g. 'equipRef->spaceRef

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">matchesTag</td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

The tag value to match e.g. 'equipRef->id'. If not set then the current entity's id is used

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">limit</td>
<td valign="top"><a href="#int"><code>Int</code></a></td>
<td>

Restrict the total number of entities returned from the search

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>tagSummary</strong></code></td>
<td valign="top">[<a href="#tagsummary"><code>TagSummary</code></a>!]!</td>
<td>

A statistical view of the tags available in the system

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">tagFilter</td>
<td valign="top">[<a href="#string"><code>String</code></a>]</td>
<td>

A list of tag names to filter

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>ref</strong></code></td>
<td valign="top"><a href="#entities"><code>Entities</code></a></td>
<td>

For each entity in this set, return the related entities linked by the nominated traversal path.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">path</td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

The path to traverse (ref or list kind) e.g. 'equipRef', or 'equipRef->siteRef'

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>units</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

Value of the 'unit' Tag if all entities match. Otherwise returns 'mixed'

</td>
</tr>
</tbody>
</table>

### `Entity`

An abstraction for some physical object in the real world.
        See https://project-haystack.org/doc/TagModel

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>description</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Description of the entity

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>id</strong></code></td>
<td valign="top"><a href="#id"><code>ID</code></a>!</td>
<td>

Identifier of the entity

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>name</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Name of the entity

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">fullyQualified</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

Name as Fully Qualified name. e.g. site.equip.point

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>search</strong></code></td>
<td valign="top"><a href="#entities"><code>Entities</code></a></td>
<td>

Search for entities with a filter that also have a Tag Value {whereTag} that matches a tag value of the current entity {matchesTag} e.g. 'equipRef->id'

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">filter</td>
<td valign="top"><a href="#haystackfilter"><code>HaystackFilter</code></a>!</td>
<td>

A Project Haystack search filter. equip and siteRef->geoCity == "Chicago" See https://project-haystack.org/doc/Filters

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">whereTag</td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Search for entities that reference the current entity by {whereTag}. e.g. 'equipRef->spaceRef'

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">matchesTag</td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

The tag value to match e.g. 'equipRef->id'. Leave empty for the current Entity id

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">limit</td>
<td valign="top"><a href="#int"><code>Int</code></a></td>
<td>

The maximum number of entities to return

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>tags</strong></code></td>
<td valign="top">[<a href="#tag"><code>Tag</code></a>!]!</td>
<td>

Lookup the tags of this entity

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">tagFilter</td>
<td valign="top">[<a href="#string"><code>String</code></a>]</td>
<td>

A list of tag names to filter

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>refEntity</strong></code></td>
<td valign="top"><a href="#entity"><code>Entity</code></a></td>
<td>

Return the neighbour entity of the nominated ref tag e.g. equipRef

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">refTag</td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

A ref tag to traverse.  e.g. 'equipRef'

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>ref</strong></code></td>
<td valign="top"><a href="#entities"><code>Entities</code></a></td>
<td>

Return the related entities linked by the nominated traversal path.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">path</td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

A path to traverse (ref or list kind) e.g. 'equipRef', or 'equipRef->siteRef'

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>history</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Retrieve the timeseries data from the entity.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">rangeAbsolute</td>
<td valign="top"><a href="#absoluterange"><code>absoluteRange</code></a></td>
<td>

The absolute date time range of the history to retrieve

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">rangeRelative</td>
<td valign="top"><a href="#relativerange"><code>relativeRange</code></a></td>
<td>

The relative Time range of the history to retrieve

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>units</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

Return the unit of measurement for this entity

</td>
</tr>
</tbody>
</table>

### `Haystack`

Query data from WideSky

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>search</strong></code></td>
<td valign="top"><a href="#entities"><code>Entities</code></a></td>
<td>

Search for entities

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">filter</td>
<td valign="top"><a href="#haystackfilter"><code>HaystackFilter</code></a>!</td>
<td>

A Project Haystack search filter

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">limit</td>
<td valign="top"><a href="#int"><code>Int</code></a></td>
<td>

Restrict the total number of entities returned from the search

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>entity</strong></code></td>
<td valign="top"><a href="#entity"><code>Entity</code></a></td>
<td>

Lookup an entity from its uuid or fully qualified name (site.equip.point)

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">id</td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

The identifier value, an uuid or fully qualified name.

</td>
</tr>
</tbody>
</table>

### `History`

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>aggregate</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Take values and aggregate them in some way

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">function</td>
<td valign="top"><a href="#aggregations"><code>aggregations</code></a>!</td>
<td>

The Boolean scalar type represents true or false

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">allEntities</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

Apply to all entities or per entity

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">groupBy</td>
<td valign="top"><a href="#groupby"><code>groupBy</code></a></td>
<td>

Group by Time

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>select</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Return one or more records based on function logic

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">function</td>
<td valign="top"><a href="#selectors"><code>Selectors</code></a>!</td>
<td>

The function logic

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">n</td>
<td valign="top"><a href="#int"><code>Int</code></a></td>
<td>

Value associated to the specified function logic

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">allEntities</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

Apply to all Entities or per Entity

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">groupBy</td>
<td valign="top"><a href="#groupby"><code>groupBy</code></a></td>
<td>

Group by Time

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>delta</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Value difference between timestamps

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">nonNegative</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

If set to true then only positive values are returned

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">allEntities</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

Apply to all entities or per entity

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">groupBy</td>
<td valign="top"><a href="#groupbyaggregate"><code>groupByAggregate</code></a></td>
<td>

Group by Time

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>movingAverage</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

The rolling average across a window of rolling periods.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">n</td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

The number of points values associated to a rolling period.
                Note: 'n' must be greater than 1.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">allEntities</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

Apply to all entities or per entity

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">groupBy</td>
<td valign="top"><a href="#groupbyaggregate"><code>groupByAggregate</code></a></td>
<td>

Group by Time

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>applyConstant</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Apply a constant. E.g. ({value} * 1000) to all values for all entities.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">math</td>
<td valign="top"><a href="#mathoptions"><code>mathOptions</code></a>!</td>
<td>

Value rank entities by their aggregated history

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>entityFilter</strong></code></td>
<td valign="top"><a href="#entities"><code>Entities</code></a></td>
<td>

Filter entities that have record count of one or more.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">rankOption</td>
<td valign="top"><a href="#rankoption"><code>rankOption</code></a></td>
<td>

Value rank entities by their aggregated history

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>numberFilter</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Filter number values based on the defined conditions

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">conditionLogic</td>
<td valign="top"><a href="#conditionlogic"><code>conditionLogic</code></a></td>
<td>

A set of conditions joined via logical OR

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">conditions</td>
<td valign="top">[<a href="#numbercondition"><code>numberCondition</code></a>]</td>
<td>

A set of conditions joined via logical OR

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>boolFilter</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Filter values based on the Bool value

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top"><code>Bool</code></td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a>!</td>
<td>

The Boolean scalar type represents true or false

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>strFilter</strong></code></td>
<td valign="top"><a href="#history"><code>History</code></a></td>
<td>

Filter str values based on the defined conditions

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">conditionLogic</td>
<td valign="top"><a href="#conditionlogic"><code>conditionLogic</code></a></td>
<td>

A set of conditions joined via logical OR

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">conditions</td>
<td valign="top">[<a href="#strcondition"><code>strCondition</code></a>]</td>
<td>

A set of conditions joined via logical OR

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>timeSeries</strong></code></td>
<td valign="top">[<a href="#timeseries"><code>TimeSeries</code></a>]</td>
<td>

The history time-series

</td>
</tr>
</tbody>
</table>

### `List`

List of zero or more values represented as strings

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>listJSON</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

JSON based list content

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>list</strong></code></td>
<td valign="top">[<a href="#tagkind"><code>tagKind</code></a>]!</td>
<td>

Formatted list content

</td>
</tr>
</tbody>
</table>

### `Marker`

A Marker the tag is merely a marker annotation and has no meaningful value. Marker tags are used to indicate a "type" or "is-a" relationship.

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>isMarker</strong></code></td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a>!</td>
<td></td>
</tr>
</tbody>
</table>

### `Number`

A Number with an optional unit of measurement

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>value</strong></code></td>
<td valign="top"><a href="#float"><code>Float</code></a></td>
<td></td>
</tr>
</tbody>
</table>

### `Ref`

Reference to another entity

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>ref</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td></td>
</tr>
</tbody>
</table>

### `Str`

A string of Unicode characters.

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>str</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td></td>
</tr>
</tbody>
</table>

### `Tag`

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>name</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Name of the tag

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>value</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

The value of the tag converted to String.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>kindValue</strong></code></td>
<td valign="top"><a href="#tagkind"><code>tagKind</code></a></td>
<td>

The unconverted value of the tag see Tag Kinds https://project-haystack.org/doc/TagModel#tagKinds

</td>
</tr>
</tbody>
</table>

### `TagSummary`

A summary view of a particular tag across multiple entities

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>count</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a></td>
<td>

Number of time the tag is defined

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>name</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Name of the Tag

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>values</strong></code></td>
<td valign="top">[<a href="#string"><code>String</code></a>]</td>
<td>

A list of values for each tag instance, converted to String.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">distinct</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td></td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>kind</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

The tag kind. E.g. Marker/String/Number...

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>kindValues</strong></code></td>
<td valign="top">[<a href="#tagkind"><code>tagKind</code></a>!]</td>
<td>

An unconverted list of values for each tag instance.

</td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">distinct</td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td></td>
</tr>
<tr>
<td colspan="2" align="right" valign="top">aggregation</td>
<td valign="top"><a href="#tagvalueaggregation"><code>tagValueAggregation</code></a></td>
<td>

Aggregate Num values

</td>
</tr>
</tbody>
</table>

### `Time`

An ISO-8601 time as hour, minute, seconds: 09:51:27.354

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>time</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td></td>
</tr>
</tbody>
</table>

### `TimeSeries`

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>dataPoints</strong></code></td>
<td valign="top">[<a href="#datapoint"><code>dataPoint</code></a>]</td>
<td>

The history data points

</td>
</tr>
</tbody>
</table>

### `Uri`

A Universal Resource Identifier

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>uri</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td></td>
</tr>
</tbody>
</table>

### `dataPoint`

<table>
<thead>
<tr>
<th align="left">Field</th>
<th align="right">Argument</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>time</strong></code></td>
<td valign="top"><a href="#unixtime"><code>UnixTime</code></a></td>
<td>

Time of the datapoint.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>value</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

Value of the datapoint converted to string.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>valueKind</strong></code></td>
<td valign="top"><a href="#pointkind"><code>pointKind</code></a></td>
<td>

Value of the datapoint converted to its actual data type.

</td>
</tr>
</tbody>
</table>

## Inputs

### `absoluteRange`

Specify an absolute time range

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>start</strong></code></td>
<td valign="top"><a href="#iso8601">iso8601</a></td>
<td>

Start time of the range (inclusive). E.g. 2019-04-29T03:00:00+00:00

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>end</strong></code></td>
<td valign="top"><a href="#iso8601">iso8601</a></td>
<td>

End time of the range (exclusive). E.g. 2019-05-10T09:00:00+00:00

</td>
</tr>
</tbody>
</table>

### `constantBySearch`

Query for an aggregated set of tag values relative to the current entity.
        See option whereTag and matchesTag for more information on how the system performs the lookup for
        relative entities.

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>filter</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

A haystack search query to further filter down the search result
                resolved using the 'whereTag' and 'matchesTag'.
                Leave blank if no further filter is needed.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>whereTag</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

This option is for telling the system how the 'relative entity' will
                be referencing the current entity.

                E.g. If the whereTag is set as "spaceRef" and the matchesTag is set as "Id".
                Then in order for an entity to be qualified as relative entity, it must;

                1) Contain the spaceRef tag
                2) The spaceRef tag value must be equvalent to the current entity's "id" tagvalue.
                Assuming matchesTag is set as "Id"

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>matchesTag</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

This option is for indicating how a relative entity will use its 'whereTag'
                value (See option whereTag) to match up with the current entity. If this is left as unset
                then the system defaults it to the "id" tagvalue.
                E.g. use case is that the whereTag is set
                as the equipRef of the point. In such case the equipRef id can then be used to find the
                relative entities that references the point's equip.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>limit</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

Limit of entities to match

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>tag</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Tag values to use for the matched entities e.g. 'area'

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>aggregation</strong></code></td>
<td valign="top"><a href="#tagvalueaggregation"><code>tagValueAggregation</code></a>!</td>
<td>

Aggregation of tags

</td>
</tr>
</tbody>
</table>

### `constantByTraverse`

Traverse to an entity by a ref tag. e.g. equipRef

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>ref</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

Return the entity of the nominated ref e.g. 'equipRef->spaceRef'. Leave blank for the current Entity

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>tag</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a>!</td>
<td>

Value to use for the traversed entity e.g. 'area'

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>aggregation</strong></code></td>
<td valign="top"><a href="#tagvalueaggregation"><code>tagValueAggregation</code></a>!</td>
<td>

Aggregation of tags

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>distinct</strong></code></td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

If true then only use an unique tag value once in the aggregation calculation.
                Example:
                If the 'tag' option is set as 'area' and a list of area value was resolved as
                 [ 100, 200, 200, 300 ].
                 If the distinct optoin is set as 'true' then the system will only use the
                 unique values from the set for aggregation.
                 That is if the 'aggregation' option is set as SUM, then the result would be 600.
                 Since 100 + 200 + 300 = 600

                 Note: This option must be used in conjuction with the "aggregation" option.

</td>
</tr>
</tbody>
</table>

### `groupBy`

Group history by a specified time interval

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>groupByUnits</strong></code></td>
<td valign="top"><a href="#duration"><code>duration</code></a>!</td>
<td>

Units to group by.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>groupBySize</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

Number of units to group by

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>fill</strong></code></td>
<td valign="top"><a href="#filloption"><code>fillOption</code></a></td>
<td>

Changes the value reported for time intervals that have no data

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>offset</strong></code></td>
<td valign="top"><a href="#timeoffset"><code>timeOffset</code></a></td>
<td>

Shifts forward or back the preset groupBy time boundaries (UTC)
                     by the nominated time duration.
                     If offset { direction:AFTER offsetUnits:MINUTES offsetSize:900 } groupByUnit = WEEK groupBySize = 1
                     The data is group by the time(UTC + 900m), the boundary is now Sunday midnight in local
                     Brisbane time.

                     Note: This option takes precedence over the offsetPointTz option.

</td>
</tr>
</tbody>
</table>

### `groupByAggregate`

Group history by a specified time interval and aggregate each interval as input for some Transformation functions

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>groupByUnits</strong></code></td>
<td valign="top"><a href="#duration"><code>duration</code></a>!</td>
<td>

Units to group by.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>groupBySize</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

Number of units to group by

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>fill</strong></code></td>
<td valign="top"><a href="#filloption"><code>fillOption</code></a></td>
<td>

Changes the value reported for time intervals that have no data

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>aggregateFunction</strong></code></td>
<td valign="top"><a href="#aggregatefunction"><code>aggregateFunction</code></a>!</td>
<td>

Aggregation method for each group.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>offset</strong></code></td>
<td valign="top"><a href="#timeoffset"><code>timeOffset</code></a></td>
<td>

Shifts forward or back the preset groupBy time boundaries (UTC) by the nominated time duration.  if offset{ direction:AFTER offsetUnits:MINUTES offsetSize:900 } groupByUnit = WEEK groupBySize = 1 The data is group by the time(UTC + 900m), the boundary is now Sunday midnight in local Brisbane time.

</td>
</tr>
</tbody>
</table>

### `mathOptions`

Apply a constant to all values

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>operator</strong></code></td>
<td valign="top"><a href="#operator"><code>operator</code></a>!</td>
<td>

Operator to apply

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>constant</strong></code></td>
<td valign="top"><a href="#float"><code>Float</code></a></td>
<td>

Constant value

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>constantByTraverse</strong></code></td>
<td valign="top"><a href="#constantbytraverse"><code>constantByTraverse</code></a></td>
<td>

Single tag value from the asset model relative to the Entity

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>constantBySearch</strong></code></td>
<td valign="top"><a href="#constantbysearch"><code>constantBySearch</code></a></td>
<td>

Aggregated tag values from the asset model relative to the Entity

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>orderSwap</strong></code></td>
<td valign="top"><a href="#boolean"><code>Boolean</code></a></td>
<td>

Swaps the order of operation. False = ({value} / {constant}) ; True = ({constant} / {value})

</td>
</tr>
</tbody>
</table>

### `numberCondition`

It allows you to group sets of condition and join them using logical conjuctions such as AND or OR.

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>operator</strong></code></td>
<td valign="top"><a href="#numbercomparisonoperator"><code>numberComparisonOperator</code></a>!</td>
<td></td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>compareValue</strong></code></td>
<td valign="top"><a href="#float"><code>Float</code></a></td>
<td>

Value to compare

</td>
</tr>
</tbody>
</table>

### `rankOption`

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>rankType</strong></code></td>
<td valign="top"><a href="#ranktypes"><code>rankTypes</code></a></td>
<td>

Type of rank

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>n</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

Number of entities to return

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>aggregation</strong></code></td>
<td valign="top"><a href="#aggregatefunction"><code>aggregateFunction</code></a>!</td>
<td>

Method to aggregate

</td>
</tr>
</tbody>
</table>

### `relativeRange`

Define a time range by specifying a duration (in the past) relative to the server's current time, e.g. now() - 1h

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>size</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

Number of time units before now()

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>timeUnit</strong></code></td>
<td valign="top"><a href="#duration"><code>duration</code></a>!</td>
<td>

End time of the range (exclusive).

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>offset</strong></code></td>
<td valign="top"><a href="#timeoffset"><code>timeOffset</code></a></td>
<td>

Offset the range

</td>
</tr>
</tbody>
</table>

### `strCondition`

It allows you to group sets of condition and join them using logical conjuctions such as AND or OR.

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>operator</strong></code></td>
<td valign="top"><a href="#strcomparisonoperator"><code>strComparisonOperator</code></a>!</td>
<td>

Operator to use in the condition

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>compareValue</strong></code></td>
<td valign="top"><a href="#string"><code>String</code></a></td>
<td>

Value to compare

</td>
</tr>
</tbody>
</table>

### `timeOffset`

<table>
<thead>
<tr>
<th colspan="2" align="left">Field</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2" valign="top"><code><strong>direction</strong></code></td>
<td valign="top"><a href="#relativeposition"><code>relativePosition</code></a>!</td>
<td>

Direction to shift

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>offsetUnits</strong></code></td>
<td valign="top"><a href="#duration"><code>duration</code></a>!</td>
<td>

Units of the duration.

</td>
</tr>
<tr>
<td colspan="2" valign="top"><code><strong>offsetSize</strong></code></td>
<td valign="top"><a href="#int"><code>Int</code></a>!</td>
<td>

Duration size

</td>
</tr>
</tbody>
</table>

## Enums

### `Selectors`

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>FIRST</strong></code></td>
<td>

Value with the oldest timestamp

</td>
</tr>
<tr>
<td valign="top"><code><strong>LAST</strong></code></td>
<td>

Value with the most recent timestamp

</td>
</tr>
<tr>
<td valign="top"><code><strong>MAX</strong></code></td>
<td>

Greatest value

</td>
</tr>
<tr>
<td valign="top"><code><strong>MIN</strong></code></td>
<td>

Lowest value

</td>
</tr>
<tr>
<td valign="top"><code><strong>TOP</strong></code></td>
<td>

Greatest N values

</td>
</tr>
<tr>
<td valign="top"><code><strong>BOTTOM</strong></code></td>
<td>

The smallest N values

</td>
</tr>
<tr>
<td valign="top"><code><strong>PERCENTILE</strong></code></td>
<td>

Nth percentile values

</td>
</tr>
</tbody>
</table>

### `aggregateFunction`

Aggregation function

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>MIN</strong></code></td>
<td>

The minimum of all records

</td>
</tr>
<tr>
<td valign="top"><code><strong>MAX</strong></code></td>
<td>

The maximum of all records

</td>
</tr>
<tr>
<td valign="top"><code><strong>MEAN</strong></code></td>
<td></td>
</tr>
<tr>
<td valign="top"><code><strong>MEDIAN</strong></code></td>
<td>

The median of all records

</td>
</tr>
<tr>
<td valign="top"><code><strong>MODE</strong></code></td>
<td>

The mode of all records

</td>
</tr>
<tr>
<td valign="top"><code><strong>SUM</strong></code></td>
<td>

The Sum of all records

</td>
</tr>
<tr>
<td valign="top"><code><strong>FIRST</strong></code></td>
<td>

The first record

</td>
</tr>
<tr>
<td valign="top"><code><strong>LAST</strong></code></td>
<td>

The last record

</td>
</tr>
<tr>
<td valign="top"><code><strong>COUNT</strong></code></td>
<td>

The number of records

</td>
</tr>
</tbody>
</table>

### `aggregations`

Aggregate functions that take values and aggregate them in some way

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>COUNT</strong></code></td>
<td>

Number of values

</td>
</tr>
<tr>
<td valign="top"><code><strong>DISTINCT</strong></code></td>
<td>

List of unique values

</td>
</tr>
<tr>
<td valign="top"><code><strong>MEAN</strong></code></td>
<td>

Arithmetic mean (average) of values

</td>
</tr>
<tr>
<td valign="top"><code><strong>MEDIAN</strong></code></td>
<td>

Middle value from a sorted list of values.  The average value of the two middle field values is returned if the field contains an even number of values.

</td>
</tr>
<tr>
<td valign="top"><code><strong>MODE</strong></code></td>
<td>

Most frequent value

</td>
</tr>
<tr>
<td valign="top"><code><strong>SPREAD</strong></code></td>
<td>

Difference between the minimum and maximum values

</td>
</tr>
<tr>
<td valign="top"><code><strong>STDDEV</strong></code></td>
<td>

Standard deviation of values

</td>
</tr>
<tr>
<td valign="top"><code><strong>SUM</strong></code></td>
<td>

Sum of values

</td>
</tr>
</tbody>
</table>

### `conditionLogic`

Logical conjunction used to check that two conditions within a group are true

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>AND</strong></code></td>
<td></td>
</tr>
<tr>
<td valign="top"><code><strong>OR</strong></code></td>
<td></td>
</tr>
</tbody>
</table>

### `duration`

Time duration

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>MILLISECOND</strong></code></td>
<td>

Millisecond (1 thousanth of a second)

</td>
</tr>
<tr>
<td valign="top"><code><strong>SECOND</strong></code></td>
<td></td>
</tr>
<tr>
<td valign="top"><code><strong>MINUTE</strong></code></td>
<td></td>
</tr>
<tr>
<td valign="top"><code><strong>HOUR</strong></code></td>
<td></td>
</tr>
<tr>
<td valign="top"><code><strong>DAY</strong></code></td>
<td></td>
</tr>
<tr>
<td valign="top"><code><strong>WEEK</strong></code></td>
<td></td>
</tr>
</tbody>
</table>

### `fillOption`

Changes the value reported for time intervals that have no data

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>LINEAR</strong></code></td>
<td>

Reports the results of linear interpolation for time intervals with no data.

</td>
</tr>
<tr>
<td valign="top"><code><strong>NONE</strong></code></td>
<td>

Reports no timestamp and no value for time intervals with no data.

</td>
</tr>
<tr>
<td valign="top"><code><strong>NULLVALUE</strong></code></td>
<td>

Reports null for time intervals with no data but returns a timestamp.

</td>
</tr>
<tr>
<td valign="top"><code><strong>PREVIOUS</strong></code></td>
<td>

Reports the value from the previous time interval for time intervals with no data.

</td>
</tr>
</tbody>
</table>

### `numberComparisonOperator`

Operators for number kind

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>EQUAL_TO</strong></code></td>
<td>

Equal

</td>
</tr>
<tr>
<td valign="top"><code><strong>NOT_EQUAL_TO</strong></code></td>
<td>

Not Equal to

</td>
</tr>
<tr>
<td valign="top"><code><strong>GREATER_THAN</strong></code></td>
<td>

Greater than.

</td>
</tr>
<tr>
<td valign="top"><code><strong>GREATER_THAN_OR_EQUAL_TO</strong></code></td>
<td>

>=

</td>
</tr>
<tr>
<td valign="top"><code><strong>LESS_THAN</strong></code></td>
<td>

<

</td>
</tr>
<tr>
<td valign="top"><code><strong>LESS_THAN_OR_EQUAL_TO</strong></code></td>
<td>

<=

</td>
</tr>
</tbody>
</table>

### `operator`

Operation to apply

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>ADD</strong></code></td>
<td>

Perform addition

</td>
</tr>
<tr>
<td valign="top"><code><strong>DIVIDE</strong></code></td>
<td>

Perform division

</td>
</tr>
<tr>
<td valign="top"><code><strong>MULTIPLY</strong></code></td>
<td>

Perform multiplication

</td>
</tr>
<tr>
<td valign="top"><code><strong>SUBTRACT</strong></code></td>
<td>

Perform subtraction

</td>
</tr>
</tbody>
</table>

### `rankTypes`

Ways to order ranking of entities

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>BOTTOM</strong></code></td>
<td>

Entities with lowest aggregation value

</td>
</tr>
<tr>
<td valign="top"><code><strong>TOP</strong></code></td>
<td>

Entities with highest aggregation value

</td>
</tr>
</tbody>
</table>

### `relativePosition`

A relative position in time

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>FORWARD</strong></code></td>
<td></td>
</tr>
<tr>
<td valign="top"><code><strong>BACK</strong></code></td>
<td></td>
</tr>
</tbody>
</table>

### `strComparisonOperator`

Operators for str kind

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>EQUAL_TO</strong></code></td>
<td>

=

</td>
</tr>
<tr>
<td valign="top"><code><strong>NOT_EQUAL_TO</strong></code></td>
<td>

â‰

</td>
</tr>
<tr>
<td valign="top"><code><strong>REGEX_MATCHES</strong></code></td>
<td>

=~

</td>
</tr>
<tr>
<td valign="top"><code><strong>REGEX_DOESNT_MATCH</strong></code></td>
<td>

!~

</td>
</tr>
</tbody>
</table>

### `tagValueAggregation`

Aggregation functions for multiple tag values

<table>
<thead>
<th align="left">Value</th>
<th align="left">Description</th>
</thead>
<tbody>
<tr>
<td valign="top"><code><strong>SUM</strong></code></td>
<td>

The Sum of all value

</td>
</tr>
<tr>
<td valign="top"><code><strong>MAX</strong></code></td>
<td>

Greatest value

</td>
</tr>
<tr>
<td valign="top"><code><strong>MIN</strong></code></td>
<td>

Lowest value

</td>
</tr>
<tr>
<td valign="top"><code><strong>MEAN</strong></code></td>
<td>

The median of all records

</td>
</tr>
</tbody>
</table>

## Scalars

### `Boolean`

The `Boolean` scalar type represents `true` or `false`.

### `Float`

The `Float` scalar type represents signed double-precision fractional values as specified by [IEEE 754](http://en.wikipedia.org/wiki/IEEE_floating_point).

### `HaystackFilter`

A Project Haystack filter e.g. equip and siteRef->geoCity == "Chicago", see https://project-haystack.org/doc/Filters

### `ID`

The `ID` scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as `"4"`) or integer (such as `4`) input value will be accepted as an ID.

### `Int`

The `Int` scalar type represents non-fractional signed whole numeric values. Int can represent values between -(2^31) and 2^31 - 1.

### `String`

The `String` scalar type represents textual data, represented as UTF-8 character sequences. The String type is most often used by GraphQL to represent free-form human-readable text.

### `UnixTime`

Number of milliseconds elapsed since 1970-01-01T00:00:00.000Z.

### `iso8601`

A dateTime represented in ISO-8601 format e.g. 2019-04-29T03:23:38+00:00 see https://en.wikipedia.org/wiki/ISO_8601
