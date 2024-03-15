---
title: sc legacy
---

# Sc Legacy

Usage: `sc legacy [flags]`

Run Sauce Connect Proxy in compatibility mode with Sauce Connect 4.9.X

**Note:** You can also specify the options as YAML, JSON or TOML file using `--config-file` flag.
You can generate a config file by running `sc legacy config-file` command.


## Server options

### `-a, --auth` {#auth}

* Environment variable: `FORWARDER_AUTH`
* Value Format: `<strings>`

Basic authentication for URL in host:port:username:password format.

### `--autodetect` {#autodetect}

* Environment variable: `FORWARDER_AUTODETECT`
* Value Format: `<value>`
* Default value: `true`

Detect the system proxy settings.
Inverse of '--no-autodetect'.
Default: true.

### `--cainfo` {#cainfo}

* Environment variable: `FORWARDER_CAINFO`
* Value Format: `<value>`
* Default value: `/private/etc/ssl/cert.pem`

CA certificate for verifying REST API.

### `--experimental` {#experimental}

* Environment variable: `FORWARDER_EXPERIMENTAL`
* Value Format: `<strings>`

Enable or disable experimental features.

### `--extra-info` {#extra-info}

* Environment variable: `FORWARDER_EXTRA_INFO`
* Value Format: `<value>`
* Default value: `{}`

JSON string that contains an advanced tunnel configuration.

### `-F, --fast-fail-regexps` {#fast-fail-regexps}

* Environment variable: `FORWARDER_FAST_FAIL_REGEXPS`
* Value Format: `<strings>`

Deny-list URL patterns.

### `--no-autodetect` {#no-autodetect}

* Environment variable: `FORWARDER_NO_AUTODETECT`
* Value Format: `<value>`
* Default value: `false`

Disable detection of the system proxy settings.
Default: false.

### `-B, --no-ssl-bump-domains` {#no-ssl-bump-domains}

* Environment variable: `FORWARDER_NO_SSL_BUMP_DOMAINS`
* Value Format: `<strings>`

Domains that do not require SSL resigning.

### `--ocsp` {#ocsp}

* Environment variable: `FORWARDER_OCSP`
* Value Format: `<value>`
* Default value: `log-only`

Cert revocation check.
One of: strict, log-only, disable.
Default: log-only.

### `--output-config-file` {#output-config-file}

* Environment variable: `FORWARDER_OUTPUT_CONFIG_FILE`
* Value Format: `<value>`

Write the new Sauce Connect 5 run command configuration to the specified file.

	If set the run command will not be executed.


### `-d, --pidfile` {#pidfile}

* Environment variable: `FORWARDER_PIDFILE`
* Value Format: `<value>`

File containing the process ID (PID).
Default: temp file.

### `-f, --readyfile` {#readyfile}

* Environment variable: `FORWARDER_READYFILE`
* Value Format: `<value>`

File containing JSON formatted metadata.
Created when the tunnel is ready.

### `-r, --region` {#region}

* Environment variable: `FORWARDER_REGION`
* Value Format: `<value>`

Sauce Labs datacenter region.
Default: us-west.

### `-x, --rest-url` {#rest-url}

* Environment variable: `FORWARDER_REST_URL`
* Value Format: `<value>`

Sauce REST API URL.
An alternative to the recommended flag '--region'.

### `-P, --se-port` {#se-port}

* Environment variable: `FORWARDER_SE_PORT`
* Value Format: `<int>`
* Default value: `-1`

Port on which Sauce Connect's Selenium relay will listen for requests.

### `-s, --shared-tunnel` {#shared-tunnel}

* Environment variable: `FORWARDER_SHARED_TUNNEL`
* Value Format: `<value>`
* Default value: `false`

Share the tunnels within the same organization.

### `--status-address` {#status-address}

* Environment variable: `FORWARDER_STATUS_ADDRESS`
* Value Format: `<value>`

Status server address in host:port format.
Default: disabled.

### `--tunnel-cainfo` {#tunnel-cainfo}

* Environment variable: `FORWARDER_TUNNEL_CAINFO`
* Value Format: `<value>`
* Default value: `/private/etc/ssl/cert.pem`

CA certificate bundle to use for verifying tunnel connections.

### `-t, --tunnel-domains` {#tunnel-domains}

* Environment variable: `FORWARDER_TUNNEL_DOMAINS`
* Value Format: `<strings>`

Domains that require tunneling.
Inverse of '--direct-domains'.

### `-i, --tunnel-name` {#tunnel-name}

* Environment variable: `FORWARDER_TUNNEL_NAME`
* Value Format: `<value>`

Tunnel name used for this tunnel or the tunnels in the same HA pool.

### `--tunnel-pool` {#tunnel-pool}

* Environment variable: `FORWARDER_TUNNEL_POOL`
* Value Format: `<value>`
* Default value: `false`

Denotes a tunnel as part of a high availability tunnel pool.

### `-u, --user` {#user}

* Environment variable: `FORWARDER_USER`
* Value Format: `<value>`

Sauce Labs username.

## Proxy options

### `-D, --direct-domains` {#direct-domains}

* Environment variable: `FORWARDER_DIRECT_DOMAINS`
* Value Format: `<strings>`

Domains that do not require tunneling.

### `-T, --proxy-tunnel` {#proxy-tunnel}

* Environment variable: `FORWARDER_PROXY_TUNNEL`
* Value Format: `<value>`
* Default value: `false`

Route all tunnel traffic through the external proxy specified in --proxy.

## DNS options

### `--dns` {#dns}

* Environment variable: `FORWARDER_DNS`
* Value Format: `<strings>`

Use the specified name server.
Example: --dns 8.8.8.8,8.8.4.4:53

## API server options

### `-k, --api-key` {#api-key}

* Environment variable: `FORWARDER_API_KEY`
* Value Format: `<value>`

Sauce Labs API Access Key.

## Logging options

### `-z, --log-stats` {#log-stats}

* Environment variable: `FORWARDER_LOG_STATS`
* Value Format: `<uint>`
* Default value: `0`

Log statistics about HTTP traffic every <seconds>.

## Options

### `-c, --config-file` {#config-file}

* Environment variable: `FORWARDER_CONFIG_FILE`
* Value Format: `<value>`

Path to YAML config file.

