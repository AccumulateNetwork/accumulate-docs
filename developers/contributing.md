---
description: >-
  This guide will walk you through setting up your environment and downloading
  the Accumulate source code.
---

# Contributing

## Prerequisites

* **Go 1.17** (or higher) is required to compile `accumulate`
* GNU Make is required to create versioned builds
* In order to capture metrics from a dev node, you must set up [Prometheus](https://prometheus.io)

If you are unsure what version of Go is installed in your environment, or you are unsure if any version is installed, use the following command to verify Go is installed:

```shell-session
$ go version
go version go1.17.x linux/amd64
```

### Go

* [Official installation guide](https://golang.org/doc/install)
* [Installing multiple versions](https://golang.org/doc/manage-install#installing-multiple)

Alternatively, on macOS you can [install Go with Homebrew](https://formulae.brew.sh/formula/go); on Linux you can install Go with your distribution's package manager. However, package managers may distribute an out of date version of Go, so direct installation is often more effective.

As described in a link above, you can use Go to install multiple versions of Go. For example, to install Go 1.17 along side an existing installation, execute these commands:

```shell-session
$ go install golang.org/dl/go1.17.2@latest
$ go1.17.2 download
$ go1.17.2 version
go version go1.17.2 linux/amd64
```

### Prometheus

* [Download from GitHub](https://github.com/prometheus/prometheus/releases)
* [Run via Docker](https://hub.docker.com/r/prom/prometheus)
* Prometheus can be installed by most package managers

Given an `accumulate` node running on 1.2.3.4 with 3000 as the base port number, Prometheus can be configured as follows:

{% code title="prometheus.yml" %}
```yaml
global:
  scrape_interval: 5s
  
scrape_configs:
  - job_name: MyBVC
    static_configs:
      - targets:
          - 1.2.3.4:3006
```
{% endcode %}

## Compiling

```shell-session
$ git clone https://github.com/accumulateNetwork/accumulate
$ cd accumulate
$ make # or go build ./cmd/accumulate
$ ./accumulate version
Accumulate network daemon v0.0.0-760-g30319a2
30319a28b59a92a82ba6cb570515cac03887effd
```
