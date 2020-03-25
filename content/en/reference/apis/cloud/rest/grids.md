---
title: "Grids"
linkTitle: "Grids"
weight: 1
Description: What are grids and how are they structured?
type: docs
---

Data in a Project Haystack server are exchanged in "grids", this is mostly a 2D tabular structure with some additional metadata tacked on.  These are then represented in either JSON or ZINC format.  The these grid formats are covered in detail under [Serialization](../serialization).

## Anatomy of a grid

Below is an example of a grid taken from the [`hisRead`](../ops/hisread`) operation page, with the text on the left showing its JSON representation, and to the top-right, the ZINC representation (with extra line breaks added for readability).  A grid can be broken down into 3 major parts:

![Anatomy of a grid](/docs/images/haystack-grid.png)

### 1. Grid Metadata

This section includes metadata which pertains to the _entire_ grid.  A good example of this would be the `ver` field, which stipulates what version of the Project Haystack standard is in use, this is a mandatory field in the grid metadata.

The above example shows two other fields, `hisStart` and `hisEnd`, both of which are `Marker`s.  Any Project Haystack data type can appear as the value for a metadata field.

### 2. Columns

The columns follow the grid metadata.  Each column has its own metadata, at minimum, includes the `name` (see 2.1 in the diagram) of the column.  In the above example, the `v0` and `v1` columns also carry an `id` metadata tag (a `Ref`), whilst the column named `ts` just carries the name of the column only.

There must be at least one column.

### 3. Rows

The actual data carried in the grid is carried in the rows of the grid.  There can be any number of rows in a grid, including zero.

## Special grids

### "Empty" grid

An empty grid is one that carries no data.  Typically, there is a "dummy" column added called `empty` to satisfy the "at least one column" requirement.

In JSON, these look like this:

```json
{
    "meta": {
        "ver": "2.0"
    },
    "cols": [
        {"name": "empty"}
    ],
    "rows": []
}
```

or as ZINC:

```
ver:"2.0"
empty

```

### Error grids

Exceptions in a Project Haystack server are reported by way of an error grid.  This looks very much like the "empty" grid above, however the metadata carries the following fields:

|Field|Kind|Value Description|
|-----|----|-----------------|
|`err`|`Marker`|Indicates that this grid carries an error message.|
|`dis`|`Str`|Human-readable error message reported by the server.|
|`errTrace`|`str`|(Optional) Stack trace of the error from the server.|

In JSON, an error grid may look like this:

```json
{
    "meta": {
        "ver":"2.0",
        "dis":"s:An Example Error Message",
        "err":"m:",
        "errTrace":"s:Stack trace of error"
    },
    "cols":[
        {"name":"empty"}
    ],
    "rows":[]
}
```

Or as ZINC:
```
ver:"2.0" dis:"An Example Error Message" err errTrace:"Stack trace of error"
empty


```

It is prudent to _always_ look for the `err` marker tag in any and all grids returned by the WideSky server before processing any other grid content.
