---
title: "dump"
weight: 2
type: docs
description: >
  `dump`: Retrieve entities from a WideSky server and write them to a file.
---

`widesky-editor dump` is a wrapper around the [`read`](../../../apis/cloud/rest/ops/read) API end-point which writes the entities out in either YAML (default) or CSV format.  The output can be either perused directly, or later loaded back in with the [`load`](../load) command.

## Usage reference

```bash
widesky-editor [-h] [--quiet] [--debug] [--log LOG] [--http-debug]
               [--uri URI] [--tls-verify TLS_VERIFY]
               [--username USERNAME] [--password PASSWORD]
               [--client-id CLIENT_ID] [--client-secret CLIENT_SECRET]
               [--impersonate-as IMPERSONATE] [--output OUTPUT]
               [--yaml] [--csv]
               dump [-h] [--id ID] [--filter FILTER]
```

* `--id ID`: Dump an entity by UUID or fully qualified name
* `--filter FILTER`: Dump entities that match the given [Project Haystack filter](https://project-haystack.org/doc/Filters)

Any number or combination of `--id` and `--filter` arguments can be given.

The output format can be selected with `--csv` or `--yaml`, and directed to a file using `--output`, generating files that conform to the [widesky-editor CSV](../../../fileformats/csv) or [widesky-editor YAML](../../../fileformats/yaml).  See [Common arguments](../common) for details.
