---
title: "Grids"
weight: 1
type: docs
description: Data serialization formats
---

## Overview
Data exchanged with the WideSky REST API is serialized in grids. Grids are two-dimensional tabular representations of tagged entities with some additional metadata. These are represented in either JSON or ZINC formats.

## Anatomy of a grid
For a detailed explination, see the Project Haystack specification for <a href="https://project-haystack.org/doc/Grids" target="_blank" rel="noopener">grids</a>

## Formats

Either ZINC or JSON formats can be used for grids. Use the Project Haystack specification links below for detailed explinations:

+ <a href="https://project-haystack.org/doc/Json" target="_blank" rel="noopener">JSON</a>
+ <a href="https://project-haystack.org/doc/Zinc" target="_blank" rel="noopener">ZINC</a>

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

```text
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
```text
ver:"2.0" dis:"An Example Error Message" err errTrace:"Stack trace of error"
empty


```
{{% alert title="Tip"  color="primary" %}}
We recommend to _always_ look for the `err` marker tag in any and all grids returned by the WideSky server before processing any other grid content.
{{% /alert %}}



### Other Resources:
Below are some helpful developer resources for handling these formats:
+ <a href="https://github.com/widesky/hszinc" target="_blank" rel="noopener">hszinc</a> for using ZINC in Python
+ WideSky Javascript client library<a href="https://github.com/widesky/jswidesky-client" target="_blank" rel="noopener">jswidesky-client</a>.
+ Project Haystack <a href="https://project-haystack.org/download#source" target="_blank" rel="noopener">source code resources</a>.
