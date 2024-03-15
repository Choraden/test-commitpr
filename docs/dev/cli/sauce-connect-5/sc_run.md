---
title: sc run
---

# Sc Run

Usage: `sc run --username <username> --access-key <UUID> --region <data center> --tunnel-name <value> [flags]`

Run Sauce Connect Proxy

**Note:** You can also specify the options as YAML, JSON or TOML file using `--config-file` flag.
You can generate a config file by running `sc run config-file` command.


## Server options

### `-k, --access-key` {#access-key}

* Environment variable: `FORWARDER_ACCESS_KEY`
* Value Format: `<UUID>`

Sauce Labs Access Key, you can get it from the User Settings page.
For additional security, we recommend setting this as an environment variable.

### `-a, --auth` {#auth}

* Environment variable: `FORWARDER_AUTH`
* Value Format: `<username[:password]@host:port,...>`

Site or upstream proxy basic authentication credentials.
The host and port can be set to "*" to match all hosts and ports respectively.
The flag can be specified multiple times to add multiple credentials.

### `-M, --metadata` {#metadata}

* Environment variable: `FORWARDER_METADATA`
* Value Format: `<key=value>,...`

Custom metadata key-value pairs.

### `-r, --region` {#region}

* Environment variable: `FORWARDER_REGION`
* Value Format: `<data center>`

Sauce Labs region name, ex.
us-west or eu-central.

### `-s, --shared` {#shared}

* Environment variable: `FORWARDER_SHARED`
* Value Format: `<all>`

Share the tunnel within the same org unit.
Only the 'all' option is currently supported.

### `-B, --tls-passthrough-domains` {#tls-passthrough-domains}

* Environment variable: `FORWARDER_TLS_PASSTHROUGH_DOMAINS`
* Value Format: `[-]<regexp>,...`

Pass matching requests to their origin server without SSL/TLS re-encryption.
You can specify --tls-passthrough-domains or --tls-resign-domains, but not both.
Prefix domains with '-' to exclude requests from being passed through.
Note that direct domains will always be passed through.

### `-b, --tls-resign-domains` {#tls-resign-domains}

* Environment variable: `FORWARDER_TLS_RESIGN_DOMAINS`
* Value Format: `[-]<regexp>,...`

Resign SSL/TLS certificates for matching requests.
You can specify --tls-resign-domains or --tls-passthrough-domains, but not both.
Prefix domains with '-' to exclude requests from being resigned.
Note that direct domains will never be resigned.

### `-T, --tunnel-domains` {#tunnel-domains}

* Environment variable: `FORWARDER_TUNNEL_DOMAINS`
* Value Format: `[-]<regexp>,...`

Forward matching requests over the Sauce Connect Proxy connection.
Requests not matching "tunnel domains" will be forwarded to their origin server over the public internet.
This is the recommended option for the best performance since it minimizes the expensive tunnelled traffic and uses it only for internal domains that are not publicly available.
You can specify --tunnel-domains or --direct-domains, but not both.
Prefix domains with '-' to exclude requests from being forwarded over the SC Proxy connection.

### `-i, --tunnel-name` {#tunnel-name}

* Environment variable: `FORWARDER_TUNNEL_NAME`
* Value Format: `<name>`

Name of the tunnel or tunnel pool.
You can run tests using this tunnel by specifying the tunnelName value in your test capabilities.

### `-t, --tunnel-pool` {#tunnel-pool}

* Environment variable: `FORWARDER_TUNNEL_POOL`
* Value Format: `<value>`
* Default value: `false`

Denotes a tunnel as part of a high availability tunnel pool.

### `-u, --username` {#username}

* Environment variable: `FORWARDER_USERNAME`
* Value Format: `<username>`

Sauce Labs username.
For additional security, we recommend setting this as an environment variable.

## Proxy options

### `-F, --deny-domains` {#deny-domains}

* Environment variable: `FORWARDER_DENY_DOMAINS`
* Value Format: `[-]<regexp>,...`

Deny requests to the matching domains.
Prefix domains with '-' to exclude requests from being denied.

### `-D, --direct-domains` {#direct-domains}

* Environment variable: `FORWARDER_DIRECT_DOMAINS`
* Value Format: `[-]<regexp>,...`

Forward matching requests to their origin server over the public internet.
Requests that don't match "direct domains" will be forwarded to customer-side over the Sauce Connect Proxy connection.
You can specify --direct-domains or --tunnel-domains, but not both.
Prefix domains with '-' to exclude requests from being forwarded directly.

### `-H, --header` {#header}

* Environment variable: `FORWARDER_HEADER`
* Value Format: `<header>`

Add or remove HTTP request headers.
Use the format "name: value" to add a header, "name;" to set the header to empty value, "-name" to remove the header, "-name*" to remove headers by prefix.
The header name will be normalized to canonical form.
The header value should not contain any newlines or carriage returns.
The flag can be specified multiple times.
Example: -H "Host: example.com" -H "-User-Agent" -H "-X-*".

### `-p, --pac` {#pac}

* Environment variable: `FORWARDER_PAC`
* Value Format: `<path or URL>`

Proxy Auto-Configuration file to use for upstream proxy selection.
It can be a local file or a URL, you can also use '-' to read from stdin.
The data URI scheme is supported, the format is `data:base64,<encoded data>`.

### `-x, --proxy` {#proxy}

* Environment variable: `FORWARDER_PROXY`
* Value Format: `[protocol://]host[:port]`

Upstream proxy to use for requests received from the Sauce Connect Server only.
The supported protocols are: http, https, socks, socks5.
No protocol specified will be interpreted as an HTTP proxy.
If the port number is not specified, it is assumed to be 1080.
The basic authentication username and password can be specified in the host string, e.g.
user:pass@host:port.
Alternatively, you can specify the credentials using the -a, --auth flag.

### `--proxy-localhost` {#proxy-localhost}

* Environment variable: `FORWARDER_PROXY_LOCALHOST`
* Value Format: `<allow|deny|direct>`
* Default value: `deny`

Setting this to allow enables sending requests to localhost through the upstream proxy.
Setting this to direct sends requests to localhost directly without using the upstream proxy.
By default, requests to localhost are denied.

### `--proxy-sauce` {#proxy-sauce}

* Environment variable: `FORWARDER_PROXY_SAUCE`
* Value Format: `[protocol://]host[:port]`

Proxy for requests to Sauce Labs REST API and Sauce Connect servers only.
See the -x, --proxy flag for more details on the format.

## DNS options

### `--dns-round-robin` {#dns-round-robin}

* Environment variable: `FORWARDER_DNS_ROUND_ROBIN`
* Value Format: `<value>`
* Default value: `false`

If more than one DNS server is specified with the --dns-server flag, passing this flag will enable round-robin selection.


### `-n, --dns-server` {#dns-server}

* Environment variable: `FORWARDER_DNS_SERVER`
* Value Format: `<ip>[:<port>]`

DNS server(s) to use instead of system default.
There are two execution policies, when more then one server is specified.
Fallback: the first server in a list is used as primary, the rest are used as fallbacks.
Round robin: the servers are used in a round-robin fashion.
The port is optional, if not specified the default port is 53.

### `--dns-timeout` {#dns-timeout}

* Environment variable: `FORWARDER_DNS_TIMEOUT`
* Value Format: `<duration>`
* Default value: `5s`

Timeout for dialing DNS servers.
Only used if DNS servers are specified.


## HTTP client options

### `--cacert-file` {#cacert-file}

* Environment variable: `FORWARDER_CACERT_FILE`
* Value Format: `<path or base64>`

Add your own CA certificates to verify against.
The system root certificates will be used in addition to any certificates in this list.
Can be a path to a file or "data:" followed by base64 encoded certificate.
Use this flag multiple times to specify multiple CA certificate files.

### `--http-dial-timeout` {#http-dial-timeout}

* Environment variable: `FORWARDER_HTTP_DIAL_TIMEOUT`
* Value Format: `<duration>`
* Default value: `30s`

The maximum amount of time a dial will wait for a connect to complete.
With or without a timeout, the operating system may impose its own earlier timeout.
For instance, TCP timeouts are often around 3 minutes.


### `--http-idle-conn-timeout` {#http-idle-conn-timeout}

* Environment variable: `FORWARDER_HTTP_IDLE_CONN_TIMEOUT`
* Value Format: `<duration>`
* Default value: `1m30s`

The maximum amount of time an idle (keep-alive) connection will remain idle before closing itself.
Zero means no limit.


### `--http-response-header-timeout` {#http-response-header-timeout}

* Environment variable: `FORWARDER_HTTP_RESPONSE_HEADER_TIMEOUT`
* Value Format: `<duration>`
* Default value: `0s`

The amount of time to wait for a server's response headers after fully writing the request (including its body, if any).This time does not include the time to read the response body.
Zero means no limit.


### `--http-tls-handshake-timeout` {#http-tls-handshake-timeout}

* Environment variable: `FORWARDER_HTTP_TLS_HANDSHAKE_TIMEOUT`
* Value Format: `<duration>`
* Default value: `10s`

The maximum amount of time waiting to wait for a TLS handshake.
Zero means no limit.

## API server options

### `--api-address` {#api-address}

* Environment variable: `FORWARDER_API_ADDRESS`
* Value Format: `<host:port>`

The server address to listen on.
If the host is empty, the server will listen on all available interfaces.

### `--api-basic-auth` {#api-basic-auth}

* Environment variable: `FORWARDER_API_BASIC_AUTH`
* Value Format: `<username[:password]>`

Basic authentication credentials to protect the server.

### `--api-idle-timeout` {#api-idle-timeout}

* Environment variable: `FORWARDER_API_IDLE_TIMEOUT`
* Value Format: `<duration>`
* Default value: `1h0m0s`

The maximum amount of time to wait for the next request before closing connection.

## Logging options

### `--log-file` {#log-file}

* Environment variable: `FORWARDER_LOG_FILE`
* Value Format: `<path>`

Path to the log file, if empty, logs to stdout.

### `--log-http` {#log-http}

* Environment variable: `FORWARDER_LOG_HTTP`
* Value Format: `[api|proxy|control:]<none|short-url|url|headers|body|errors>,...`

HTTP request and response logging mode.
Setting this to none disables logging.
The short-url mode logs [scheme://]host[/path] instead of the full URL.
The error mode logs request line and headers if status code is greater than or equal to 500.

### `--log-level` {#log-level}

* Environment variable: `FORWARDER_LOG_LEVEL`
* Value Format: `<error|info|debug>`
* Default value: `info`

Log level.

