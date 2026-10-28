# unicorn-device-common

Binary release of the shared device-side Unicorn foundation: the
`unicorn-agentd` protected-data agent, `unicorn-inventoryd`, and the
`libunicorn_client` shared library for AOSP device images.

## Layout

- `prebuilt/armeabi-v7a/` - device binaries
- `aosp/init/` - init.rc fragments for the daemons
- `LICENSE` - binary EULA (proprietary; no source distributed)

## Required device configuration

The daemons will not function without the bootstrap configuration under
`/system/etc/unicorn/`:

- `agent_config.cbor` - CBOR bootstrap record carrying the service CA
  bundle and `service_url` (HTTPS endpoint of the customer service)
- `authorized_packages.txt` - package allowlist for app authorization
- `service-ca.pem` - private service CA certificate
- `prefetch.list` (optional) - startup prefetch tuples, one
  `<operation> <base64 family> <base64 logical-data-id>` per line

Device state lives at `/data/misc/unicorn/state`; both daemons run as
`system` and restart via init. The `unicorn-agentd` executable digest is
pinned by the issued ROM policy — any replacement binary requires a
ROM-policy re-issue before enrollment succeeds.

All artifacts are released under the terms in LICENSE.
