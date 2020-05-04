---
title: "Query Builder"
linkTitle: "Query Builder"
weight: 3
type: docs
description: >
    A friendly interface that allows you to build sophisticated WideSky queries without typing
---
The WideSky query builder provides an interactive interface to build Grafana dashboards and panels. Built specifically for Grafana, you can build sophisticated insights without having to reference the GraphQL API docs or worry about query syntax errors. Queries can range in complexity from a simple count of entities with the `site` tag, to complex time series aggregations or transformations.

## Query builder
<video  width=70% autoplay controls loop muted playsinline>
  <source src="/docs/videos/widesky-query.mp4" type="video/mp4">
</video>

<!--
## Accessing the builder

You can access the WideSky query builder when you are in the edit mode of a Panel. By default, when you create a new panel, a basic query is pre-filled automatically.

<video  width=70% autoplay controls loop muted playsinline>
  <source src="/docs/videos/widesky-new-query.mp4" type="video/mp4">
</video>
-->
---

## Core Concepts

Below are some core concepts that are helpful to know when building a query.

### Objects and Fields
A WideSky GraphQL query is constructed by asking for specific fields on objects. To assist common data analytics problems and to leverage Project Haystack semantic modelling, we've built many custom fields and object types.

Each object type has one or many fields available that can return basic types, e.g. Bool or string, or a complex types, e.g. timeseries data. When you build a query you need to specify the fields you need, the query builder presents the available fields choices based on the object type.

Let's look at a simple example. All fields appear on the left, colored <span style="color:blue">*blue*</span>.

![Simple entity query](/docs/images/widesky-query-site-count.png)

You can see that we query for 3 fields:
+ **haystack**: Each query must begin with this field.
+ **search**: A sub-field of **haystack**, search uses a Project Haystack filter, in this case 'point' to search WideSky Entities with the tag `point`.
+ **count**: A sub-field of **search**, count return with the number of entities returned in the search. In our case, it's 4.

Let's look at a query that plots timeseries data:

![Simple timeseries example](/docs/images/widesky-query-simple-timeseries.png)

You can see that we query for 4 fields:
+ **haystack**: Each query must begin with this field.
+ **search**: A sub-field of **haystack**, search uses a Project Haystack filter, in this case 'point and his and power' to search WideSky Entities with the tags `point`, `his` and `power`.
+ **history**: A sub-field of search, that's used to access history data of the `point` entities.
+ **timeseries**: A sub-field of history, which returns the timeseries data. In our case, we get 4 series.

{{% alert title="Tip"  color="primary" %}} For most Grafana panels that visualise timeseries data, e.g. the graph panel. You need to construct a query that contains the timeseries field for the panel to display anything.
{{% /alert %}}

You can freely add and remove fields to alter what data you can request from WideSky in a single query. Overall there are 19 custom object types, the 6 main types are in the following table:

|Object|# of Available Fields|Description|
|------|--------------------------|-----------|
|[**Haystack**](/docs/reference/apis/cloud/graphql/schema/#haystack)|2|The Root Object - Each query must start with this object|
|[**Entities**](/docs/reference/apis/cloud/graphql/schema/#entities)|7|A collection of 1 or more Project Haystack Entities|
|[**Entity**](/docs/reference/apis/cloud/graphql/schema/#entity)|9|A single Project Haystack Entity|
|[**History**](/docs/reference/apis/cloud/graphql/schema/#history)|10|The timeseries history of an entity. *Note: The entity must satasify several conditions to have history*|
|[**Timeseries**](/docs/reference/apis/cloud/graphql/schema/#timeseries)|1|Timeseries datapoints|
|[**Tag**](/docs/reference/apis/cloud/graphql/schema/#tag)|3|Tagging information of an entity|

View the [Schema Reference](/docs/reference/apis/cloud/graphql/schema/), or the [Interactive view](/docs/reference/apis/cloud/graphql/interactive-graph/) to see the entire GraphQL schema.

{{% alert title="Tip"  color="primary" %}}
The [GraphQL interacive view](/docs/reference/apis/cloud/graphql/interactive-graph/) provides a good visual representation of the objects, fields, and how they relate.
{{% /alert %}}

#### Adding fields

To add a field, click on an existing field to access the pop-up menu under 'fields' and select one from a list.

<video  width=70% autoplay controls loop muted playsinline>
  <source src="/docs/videos/widesky-query-fields.mp4" type="video/mp4">
</video>

{{% alert title="Tip"  color="primary" %}} Hover over the info icon in the fields menu to see a documentation snippet.
{{% /alert %}}


#### Changing fields
To alter a field, click on an existing field and drill down to 'change to' to see a list of available fields.

{{% alert title="Warning"  color="warning" %}} When changing fields, arguments and sub-fields that also exist on the replacement field remain in your query. All other incompatible arguments and sub-fields are removed.
{{% /alert %}}

#### Removing fields
To remove a field, click on an existing field and select 'remove'. All arguments and sub-fields are deleted.


### Arguments
Each field can have one or more arguments which alter the behaviour of a field. Mandatory arguments are placed in-line with the field and require a value to be set. Non-mandatory arguments are initially collapsed under 'options'. Click on the options arrow to expand them and set their values. Arguments with a default value appear as are shown in grey. An argument can also have nested arguments which are also initially collapsed.

<video  width=70% autoplay controls loop muted playsinline>
  <source src="/docs/videos/widesky-query-arguments.mp4" type="video/mp4">
</video>


### Time range

The start and end times of the dashboard are exposed as the variables `$to` and `$from`. To ensure the time range of the query matches the Grafana dashboard, these variables are automatically entered into the `relativeRange` arguments of the `history` field when it's added.

![Time rage arguments](/docs/images/widesky-query-timerange.png)

---

## Haystack filter auto-complete

The query builder has auto-complete functionality to assist the construction of the [Project Haystack filter](https://project-haystack.org/doc/Filters) argument. It offers contextually aware choices after each edit allowing you to query for tags in your asset model without prior knowledge of what's available.

<video  width=70% autoplay controls loop muted playsinline>
  <source src="/docs/videos/widesky-query-filter.mp4" type="video/mp4">
</video>

To create a filter, click the `select a tag` button to the right of the `filter` field and select a tag. Depending on the selected [tag kind](https://project-haystack.org/doc/TagModel#tagKinds) the builder suggests choices for the next part of the filter.

You can remove parts of a filter by clicking either an operator `and` `or`, comparison operator `==`, `!=`, or path `->` and then selecting `--Remove--`. The right side of the statement up to the next comparison operator will be deleted.

{{% alert title="Tip"  color="primary" %}} Manually type a filter to build more complex queries with parentheses e.g. `point and (power or energy)`.
{{% /alert %}}


---

## Query formats

Change the query format to suit panels by clicking on `Format as` and selecting a mode in the table below:


|Mode|Description|
|------|-----------|
|*Time Series*|Used for most panels types to plot data over time, e.g. Graph panel|
|*Table*|Used for Table or Worldmap panels|
|*WideSky*|Used for WideSky real-time control button|


### Time series Format

Use the time series format option for panels that plot data over time. A `timeSeries` field (sub-field of history) is also required your query.

{{% alert title="Tip"  color="primary" %}} Always have a select or aggregation function that has groupBy arguments set, otherwise, WideSky can easily return hundreds of thousands of data points that and hang the browser.
{{% /alert %}}

#### Auto GroupBy

When there are more data points than can be shown on a graph, the queries can be made more efficient by grouping by a larger time interval. The builder sets the variables `__intervalDuration` and `__intervalNum` to the Grafana auto-calculated time interval. These variables are automatically entered into the *aggregate* or *select* fields arguments.



#### Alias

By default, if alias setting is blank, the panel labels each series found in the query response with an auto-generated name.

To define a label for your series, you can either:
 - Set a static name for the series by setting a value.
 - Use data from another field in your query by specifying a path to the field.
 - A mixture of both points above.

{{% alert title="Tip"  color="primary" %}} The auto generated series name will search for `description` fields if the alias setting is blank.
{{% /alert %}}

##### Path syntax

You can specify what field(s) to alias by specifying the path of the field relative to the `timeSeries` field in your query. This path uses a simple relative path syntax encapsulated in braces `{<relative path from timeSeries to field>}`.

|Syntax|Description|
|------|-----------|
|`./`|Means the current field|
|`../`|The parent field of the current `timeSeries` field|
|`../../`|The field that is two levels above the current `timeSeries` field|
|`../<field_A>`|The sub-field `<field_A>` of the current `timeSeries` field|
|`../{<field_A>[n].<field_B>}`|The sub-field field_B from the nth element of sub-field`field_A`, of the current `timeSeries` field. Array indexes start at 0.|



##### Path example
Given the query:

![Alias example](/docs/images/widesky-query-alias.png)

Example alias configurations:

|Alias value|Resulting series label|
|------|-----------|
|`MSB North`|MSB North|
|{../../description}|\<asset model entity description\> e.g. Active Energy|
|`MSB North {../../description}`|MSB North Active Energy|
|`{../../refEntity/description} MSB North {../../description}`|Site A MSB North Active Energy|


### Table format

When `Format as` is set to table, the builder presents a column selector. Click on `select field` to assign a field to a column.

All field values are shown using a relative path, e.g. `haystack.search.count`. Subsequent columns can be flattened to a parent columns if the sub-field has multiple values. You can flatten fields with more than one result to a parent field, by selecting the parent field in `flatten with`.

<video  width=80% autoplay controls loop muted playsinline>
  <source src="/docs/videos/widesky-query-table.mp4" type="video/mp4">
</video>

{{% alert title="Tip"  color="primary" %}} When building a table panel, add a column style under the Visualization tab to override the column name or change formatting.
{{% /alert %}}

---

## Mode switch

You can switch to text edit mode by clicking the pencil icon. This mode allows you edit the GraphQL query directly.

{{% alert title="Tip"  color="primary" %}} Use the mode switch to copy / paste queries between panels.
{{% /alert %}}

---

<!-- Not complete yet
## Advanced queries

We've structured the WideSky GraphQL API to provide maximim felxability allowing you to nest fields for asset model walking, or perform data transformation on single or multiple entites in a single request.

{{% alert title="Tip"  color="primary" %}}
There is no limit to the amount of information or combination of fields and objects you can request in a single GraphQL query. This includes both asset model and time series data. WideSky, however, limits the execution time of a query to prevent server overloading. For example, Large time series queries without sufficient time windowing, e.g. Group By Day.
{{% /alert %}}

### Recusive search example

In this example we'll count how many elec meters are located in each space.

See the example below:

(image)

1. The `seach` field on the Haystack object return the `Entities` object.
2. The `Entities` object also has a `search` field that allow you to search for entities based on the current entity set.
3. We can now count how many meters are located in each space


### Timeseies transformation example

Continuing the recuesive search example above, we'd like to sum each meter to obtain a trend of each space energy usage. As each meter records energy in a accumulator , denoted bu the `hisTotalized` tag, we need to perform a delta operation on the indivial meters. After performing the delta, we then perform a sum, but set the AllEntities attribute to true.

(image, delta 2 meters then sum)


1. For each meter at each sace, obtain the Hstory
2. Perform a delta operation
3.

The `seach` field on the Haystack object return the `Entities` object. The `Entities` object also has a `search` field that allow you to search for entities based on the current entity set.
-->
