# Secure Shell runtime options

The Secure Shell program supports a number of command line flags to control
behavior on a per-connection basis.  These are not to be confused with the
various terminal preferences (like colors or fonts).

## `--config=<name>`

This is a shortcut for setting other options so people don't have to remember
the full list.  At the moment, the only config supported is `google`.

## `--proxy-host=<host>`

The host to use as a relay server.  All connections will be made via this
server.

## `--proxy-port=<port>`

The port to connect to on the relay server.

## `--use-ssl=<bool>`

Whether to use HTTPS (the default) or HTTP when communicating with the relay
server.

Even if you use HTTP, the actual ssh session will still be encrypted.

## `--use-xhr`

Use XML HTTP requests (XHR) when communicating with the relay server instead of
WebSockets.  Use of this depends on your relay server implementation.

## `--report-ack-latency`

Report ACK latency to the relay server.
If you don't know what this is for, then just ignore it.

## `--report-connect-attempts`

Report connection attempt counts to the relay server.
If you don't know what this is for, then just ignore it.

## `--ssh-agent=<backend ID>,<backend ID>,...`

A comma-separated list of IDs of backends to use with the builtin JS SSH agent.
All agent requests are sent to all backends and their results are accumulated
and relayed back to the client.

The following backends are currently implemented:
* `stub`:
  A minimal implementation of a backend. Only used for testing purposes.
* `gsc`:
  Supports SSH authentication using private keys stored on
  OpenPGP-enabled smart cards. **Note:** Requires the
  [Smart Card Connector app](https://chrome.google.com/webstore/detail/khpfeaanjngmcnplbdlpegiifgpfgdco)
  to be installed.

## `--ssh-agent=<extension id>`

The extension to use as an ssh agent.  All auth requests will be forwarded
from the ssh session to this extension for processing.  It can be used to
manage keys or certificates or anything else an ssh agent can.

Here's a list of known agents:

* [gnubbyd beknehfpfkghjoafdifaflglpjkojoco](https://chrome.google.com/webstore/detail/beknehfpfkghjoafdifaflglpjkojoco)

## `--ssh-client-version=<version>`

The version of the ssh client to use.  Intended for mitigating regressions with
newer versions of the plugin and quick version comparison.

Support for older versions is not permanent and there is no guarantee that newer
releases will continue to bundle them.  If you encounter problems with the
default version and selecting a previous version makes things work, you need to
[report a bug](https://goo.gl/vb94JY).

Here are some versions that might be available:

* `pnacl`: The default OpenSSH version built for NaCl most people should use.
* `pnacl-openssh-7.5p1`: An older OpenSSH release.
