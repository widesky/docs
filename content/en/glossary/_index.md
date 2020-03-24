---
title: "Glossary"
weight: 3
type: docs
breadcrumb_disable: true
title_disable: true
tree_nav_disable: true
menu:
  main:
    weight: 3
---

# Glossary
|Term|Definition|
|-----------------------------|-----------|
|<img width=400/>Asset Model|A collection of entities  and the relationship between them. These things could be pieces of equipment, sensors within a piece of equipment, a location grouping things together, basically any physical object can be represented and within the Asset Model, an object is referred as the term entity.|
|CSV|Comma-Separated Values, a basic flat-file format for representing tabular data which is compatible with spreadsheeting applications.|
|Entity|A distinct representation of a physical or virtual thing.  You can think of an entity an abstraction for single Site (a building with an address), a piece of equipment in a building (e.g. HVAC unit, an electric meter, or a variable air volume box), or a sensor point (Digital or analogue sensor that generate signals and data e.g. temperature sensor, pressure sensor, on/off switch, etc).|
|Fully Qualified Name|A fully qualified name (`fqname`) is a string identifier of an entity. representing the entire hierarchy of an entity, separated by dots.|
|Grafana|[Grafana](https://www.grafana.com) is an open source analytics and visualization solution. WideSky Cloud comes with a managed Grafana instance that includes a feature-rich data plug-in for WideSky.|
|Grid|Grids are two-dimensional tabular representations of tagged entities.|
|`id`|`id` is a tag that is used to model the unique identifier of an entity in system. id tags in WideSky must be a uuid. Upon creation  ID's are assigned if not specified. After creation, an entities fqname, if available, can also be substituted.|
|`name`|`name` is a special String tag that is used to identify an Entity via `fqname`. The `name` tag must be unique all root-level entities, or all entities sharing the same parent (e.g. for every `site` entity or amongst entities with the same `siteRef` or `equipRef`)|
|op or ops|An operation is a specific URI within the WideSky Cloud REST API that receives a request and returns a response.|
|Primary tag|A primary tag of marker type that defines they primary type of entity. Every entity in WideSky must have only one of the following primary tags defined upon creation: <ul><li>`account`</li><li>`actionPolicy`</li><li>`application`</li><li>`connection`</li><li>`equip`</li><li>`network`</li><li>`point`</li><li>`precinct`</li><li>`role`</li><li>`site`</li><li>`space`</li><li>`user`</li><li>`weather`</li><li>`wsgService`</li></ul>|
|Project Haystack|An open source [initiative](https://project-haystack.org/) to streamline working with data from the Internet of Things. WideSky cloud implement Haystack entities, tagging, and the standardized REST API.|
|tag|A tag is a name/value pair applied to an entity that defines a fact or attribute about an entity. For example,  the site tag declares an entity represents a building that has an address as per the Project - Haystack definition of the site tag.|
|Tag Kind| A tag kind is one of the permitted value types of a tag. WideSky has adopted the [Project Haystack tag kinds](https://project-haystack.org/tag/kind).  The following tag kinds are currently supported in WideSky: <ul><li>`Marker`: the tag is merely a marker annotation and has no meaningful value. Marker tags are used to indicate a _type_ or _is-a_ relationship.</li><li>`Bool`: boolean `true` or `false`.</li><li>`Number`: integer or floating point number annotated with an optional unit of measurement.</li><li>`Str`: a string of Unicode characters.</li><li>`Uri`: a Universal Resource Identifier.</li><li>`Ref`: a reference to another entity with an optional description.</li><li>`Bin`: a binary blob with a MIME type.</li><li>`Date`: an [ISO 8601 date](https://en.wikipedia.org/wiki/ISO_8601#Dates) as year, month, day: `2011-06-07`.</li><li>`Time`: an [ISO 8601 time](https://en.wikipedia.org/wiki/ISO_8601#Times) as hour, minute, seconds: `09:51:27.354`.</li><li>`DateTime`: an [ISO 8601 timestamp](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations) followed by time-zone name.</li><li>`Coord` geographic coordinate in latitude/longitude.</li><li>`List`: heterogenous list of zero or more values.</li></ul>|
|Thread|[Thread](https://www.threadgroup.org/) is an IPv6-based, low-power mesh networking technology for IoT products, intended to be secure and future-proof.|
|Time series data|Time-series data is data that is recorded over a period of time, with each recording being associated with a timestamp. A value (can be either in type String, Boolean or Floating numbers).|
|UUID|[Universally Unique Identifier](https://tools.ietf.org/html/rfc4122). A 128-bit number used to identify an entity in WideSky.|
|widesky-editor|widesky-editor is a tool for manipulating entities in WideSky. With editor you can dump edit and load entity configurations at scale.|
|ZINC|Zinc stands for "Zinc Is Not CSV". Zinc is a plaintext syntax for serializing Haystack grids using a souped up CSV format.|
