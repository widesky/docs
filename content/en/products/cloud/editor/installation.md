---
title: "Install Editor"
linkTitle: "Install Editor"
weight: 1
type: docs
description: >
  How to install WideSky Editor
---
You can run Editor on macOS, Windows, and 64-bit Linux.

## Prerequisites

+ Editor currently ships as a Docker container that is run from a small bash script wrapper. Use the <a href="https://docs.docker.com/install/" target="_blank" rel="noopener">Docker Installation Guide</a> to install docker for your system.
+ Windows systems will also need the Windows Subsystem for Linux (WSL). See the <a href="https://docs.microsoft.com/en-us/windows/wsl/install-win10" target="_blank" rel="noopener">Windows Subsystem for Linux Installation Guide</a>



{{% alert title="Tip"  color="primary" %}}
For Windows users:
+ Use [this guide](https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly) to assist your installation.
+ When dumping and loading files from your system, the files locations need to be accessable by docker, e.g. your working path needs to start with `/c` or `/d` see [this bug](https://github.com/docker/for-win/issues/2151) for details.
{{% /alert %}}


## Installation

To install editor run this command:

```bash
sudo curl -L --fail https://raw.githubusercontent.com/widesky/editor/master/runners/widesky-editor.sh -o /usr/local/bin/widesky-editor;
sudo chmod +x /usr/local/bin/widesky-editor
```


To test WideSky editor:

```bash
widesky-editor --help
```
{{% alert title="Note"  color="primary" %}} The first run may take longer than normal as the Docker container downloads.
{{% /alert %}}


You should see the following output:
```bash
usage: widesky-editor [-h] [--quiet] [--debug] [--log LOG] [--http-debug]
                      [--uri URI] [--tls-verify TLS_VERIFY]
                      [--username USERNAME] [--password PASSWORD]
                      [--client-id CLIENT_ID] [--client-secret CLIENT_SECRET]
                      [--output OUTPUT] [--yaml] [--csv]
                      {dump,load} ...

Widesky model editing tool

positional arguments:
  {dump,load}           sub-command help
    dump                Dump entity information from the server
    load                Load entity changes into the server

optional arguments:
  -h, --help            show this help message and exit
  --quiet               Operate quietly, no output
  --debug               Show debugging information
  --log LOG             Log output
  --http-debug          Show HTTP debugging information
  --uri URI             Server address
  --tls-verify TLS_VERIFY
                        Do we validate the TLS certificate? Either give a path
                        to the CA's certificate, to validate against a
                        specific CA, or if set to "skip"to skip validation.
  --username USERNAME   Log-in username
  --password PASSWORD   Log-in password
  --client-id CLIENT_ID
                        Log-in client ID
  --client-secret CLIENT_SECRET
                        Log-in client secret
  --output OUTPUT       Output file
  --yaml                Output data in YAML format.
  --csv                 Output data in CSV format.
```

## Upgrading

To upgrade you need to pull the latest container. Run the following command:

```bash
docker pull wideskycloud/editor;
```


## Uninstallation

To uninstall WideSky Editor:

```bash
sudo rm /usr/local/bin/widesky-editor;
docker image rm wideskycloud/editor;
```
