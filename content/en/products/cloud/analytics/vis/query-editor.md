---
title: "Query Editor"
linkTitle: "Query Editor"
weight: 3
type: docs
description: >
  How to use WideSky in Grafana.
---

WideSky uses GraphQL to provide a powerful interface to construct data insights. The the query editor provides a friendly interface that allows you to build a GraphQL query without typing.

You can access the WideSky query editor when you are in the edit mode of a Panel. By default, when you create a new panel a basic query will be pre-filled.

![An example WideSky query](/docs/images/widesky-query-new.gif)


## Core Concepts

Below are some core concepts that are helpful to know when building a query,

### Fields
A WideSky query is constructed by asking for specific fields. To construct a query for Grafana to plot, you need to add fields that will return with data for the panel to display. All fields appear on the left of the editor colored <span style="color:blue">*blue*</span>.

#### Adding fields

To add a field, click on an existing field to access the pop-up menu under 'fields' and select one from a list.

{{% alert title="Tip"  color="primary" %}} Hover over the info icon in the fields menu to see a documentation snippet.
{{% /alert %}}

![Select fields to form a query](/docs/images/widesky-query-fields.gif)

#### Changing fields
To alter a field, click on an existing field and drill down to 'change to' to see a list of available fields.

{{% alert title="Warning"  color="warning" %}} When changing a fields, arguments and sub-fields that also exist on the replacement field will remain. All other incompatible arguments and sub-fields will be removed.
{{% /alert %}}

#### Removing fields
To remove a field, click on an existing field select 'remove'. All arguments and sub-fields will also be deleted.


### Arguments
Each field can have one or more arguments that are used to alter the behavior of a field. Mandatory arguments that require you to select a value appear in-line with the field. Non-mandatory arguments will initially be collapsed under 'options'. Click on the options arrow to expand them and set their values. Arguments with default values will be shown in gray. An argument can also have nested arguments.

![Set arguments to refine your query](/docs/images/widesky-query-arguments.gif)

### Time range

The start and end times of the dashboard are exposed as the variables `$to` and `$from`. To ensure the time range of the query matches the Grafana dashboard, these variables are automatically entered into the `relativeRange` arguments of the `history` field when it's added.

![Time rage arguments](/docs/images/widesky-query-timerange.png)


## Haystack filter auto-complete

The query editor has auto-complete functionality to assist construction of the [Project Haystack filter](https://project-haystack.org/doc/Filters) argument. It will offer contextually aware choices after each edit. This allows you to query for tags in your asset model without prior knowledge of what's available.

![Haystack filter auto-complete](/docs/images/widesky-query-filter.gif)

To create a filter, click the `select a tag` button to the right of the `filter` field and select a tag. Depending on the selected [tag kind](https://project-haystack.org/doc/TagModel#tagKinds) the editor will suggest choices for the next part of the filter.

You can remove parts of a filter by clicking either an operator `and` `or`, comparison operator `==`, `!=`, or path `->` and then selecting `--Remove--`. The right side of the statement until the next comparison operator will be deleted.

{{% alert title="Tip"  color="primary" %}} Manually type a filter to build more complex queries with parentheses e.g. `point and (power or energy)`.
{{% /alert %}}

## Query formats

Change the query format to suit panels by clicking on `Format as` and selecting a mode in the table below:


|Mode|Description|
|------|-----------|
|*Time Series*|Used for most panels types to plot data over time e.g. Graph panel|
|*Table*|Used for Table or Worldmap panels|
|*WideSky*|Used for WideSky real-time control button|


### Time series Format

Use the time series format option for panels that plot data over time. A `timeSeries` field (sub-field of history) is also required your query.

{{% alert title="Warning"  color="warning" %}} Please always have a select or aggregation function that has groupBy arguments set, otherwise WideSky can easily return hundreds of thousands of data points that will hang the browser.
{{% /alert %}}

#### Auto GroupBy

When there are more data points than can be shown on a graph, the queries can be made more efficient by grouping by a larger interval. The editor sets the variables `__intervalDuration` and `__intervalNum` to the auto calculated interval. These variables are automatically entered into the `aggregate` or 'select' fields when they're added.



#### Alias

By default, if alias setting is blank the panel will label each series found in the query response with an auto generated name.

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
|`../{<field_A>[n].<field_B>}`|The sub-field field_B from the nth element of sub-field`field_A`, of the current `timeSeries` field|



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

When `Format as` is set to table, the editor presents a column selector. Click on `select field` to assign a field to a column.

All field values are shown using a relative path e.g. `haystack.search.count`. Subsequent columns can be flattened to a parent columns if the sub-field has multiple values. You can flatten fields with more than one result to a parent field, by selecting the parent field in `flatten with`.

![Table Builder](/docs/images/widesky-query-table.gif)

{{% alert title="Tip"  color="primary" %}} When building a table panel, add a column style under the Visualization tab to override the column name or change formatting.
{{% /alert %}}


### Mode switch

You can switch to text edit mode by clicking the pencil icon. This mode allows you edit the GraphQL query directly.
