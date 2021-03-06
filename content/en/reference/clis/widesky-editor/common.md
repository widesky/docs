---
title: "Common arguments"
weight: 1
type: docs
description: >
  Common command line arguments for `widesky-editor`
---

This section details the command line arguments which are common to both `dump` and `load` commands.

## Usage reference

```bash
widesky-editor [-h] [--quiet] [--debug] [--log LOG] [--http-debug]
               [--uri URI] [--tls-verify TLS_VERIFY]
               [--username USERNAME] [--password PASSWORD]
               [--client-id CLIENT_ID] [--client-secret CLIENT_SECRET]
               [--impersonate-as IMPERSONATE] [--output OUTPUT]
               [--yaml] [--csv]
```

### Logging-related arguments

* `--quiet`: Silence the chatter whilst processing commands
* `--debug`: Enable debug-level chatter whilst processing commands (ignored if `--quiet`)
* `--log LOG`: Direct logging output to a file named `LOG`
* `--http-debug`: Enable low-level HTTP debugging

In the event that authentication fails, `--debug --http-debug` can be useful to see what went wrong.

### WideSky server URI and credentials

* `--uri URI`: Sets the base address of the WideSky server, e.g. `https://example.on.widesky.cloud/widesky/`
* `--username USERNAME`: Sets the user name for authentication
* `--password PASSWORD`: Sets the password for authentication
* `--client-id CLIENT_ID`: Sets the client ID
* `--client-secret CLIENT_SECRET`: Sets the client secret
* `--impersonate-as IMPERSONATE`: Tells the WideSky server to "impersonate" another user.  `IMPERSONATE` should be set to the UUID of the user to impersonate.  `USERNAME` (see `--username`) will require `IMPERSONATE` privileges.

Of these, `--uri`, `--username`, `--password`, `--client-id` and `--client-secret` are required for all operations.

### Output mode selection and redirection

* `--output OUTPUT`: Writes the output of the command to a file instead of standard output.
* `--csv`: Use [CSV format](../../../fileformats/csv/) for output
* `--yaml`: Use [YAML format](../../../fileformats/yaml/) for output (default)
