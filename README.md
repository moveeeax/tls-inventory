# tls-inventory

> Every certificate you own, in one table, before one of them expires.

**Status:** 🚧 In development

## Overview

Crawl a domain list and report certificate chain, expiry, issuer, protocol versions and cipher suites in one table, with a CI-friendly exit code.

## Features

- Walks a domain or host:port list concurrently and reports the full presented chain, not only the leaf
- Reports days to expiry per certificate and flags anything inside a configurable threshold
- Detects incomplete chains, self-signed leaves, hostname mismatches and expired intermediates
- Negotiates each protocol version separately, so TLS 1.0 and 1.1 still being offered shows up
- Lists accepted cipher suites and marks the ones without forward secrecy
- Exits non-zero on policy violations so it can sit in a scheduled pipeline, with JSON output for the dashboard

## Stack

Go + crypto/tls and crypto/x509 from the standard library, cobra, golang.org/x/sync/errgroup for concurrency, and olekukonko/tablewriter for output.

## Usage

```bash
tls-inventory --hosts ./domains.txt --expiry-warn 30d \
  --min-version tls1.2 --concurrency 50 --format table --fail-on warn
```

## License

MIT
