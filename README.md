<p align="center">
<a href="https://github.com/sauljabin/kaskade"><img alt="kaskade" src="https://raw.githubusercontent.com/sauljabin/kaskade/main/screenshots/banner.png"></a>
</p>
<a href="https://github.com"><img alt="GitHub" width="60" height="20" src="https://img.shields.io/badge/-github-blueviolet?logo=github&logoColor=white"></a>
<a href="https://github.com/sauljabin/kaskade/blob/main/LICENSE"><img alt="MIT License" src="https://img.shields.io/github/license/sauljabin/kaskade"></a>
<a href="https://github.com/sauljabin/kaskade/actions"><img alt="GitHub Workflow Status" src="https://img.shields.io/github/actions/workflow/status/sauljabin/kaskade/main.yml?branch=main"></a>
<a href="https://app.codecov.io/gh/sauljabin/kaskade"><img alt="Codecov" src="https://img.shields.io/codecov/c/github/sauljabin/kaskade"></a>
<br>
<a href="https://www.python.org/"><img alt="Python" width="60" height="20" src="https://img.shields.io/badge/-python-brightgreen?logo=python&logoColor=white"></a>
<a href="https://pypi.org/project/kaskade"><img alt="Version" src="https://img.shields.io/pypi/v/kaskade"></a>
<a href="https://pypi.org/project/kaskade"><img alt="Python Versions" src="https://img.shields.io/pypi/pyversions/kaskade"></a>
<a href="https://pypi.org/project/kaskade"><img alt="Platform" src="https://img.shields.io/badge/platform-linux%20%7C%20osx-0da5e0"></a>
<br>
<a href="https://kafka.apache.org/"><img alt="Kafka" width="60" height="20" src="https://img.shields.io/badge/-kafka-e3e3e3?logo=apache-kafka&logoColor=202020"></a>
<a href="https://pypi.org/project/confluent-kafka/"><img alt="Kafka Client" src="https://img.shields.io/pypi/v/confluent-kafka?label=client">
<a href="https://kafka.apache.org/"><img alt="Kafka" src="https://img.shields.io/badge/kafka-3.x-blue"/></a>
</a>
<br>
<a href="https://www.docker.com/"><img alt="Docker" width="60" height="20" src="https://img.shields.io/badge/-docker-blue?logo=docker&logoColor=white"></a>
<a href="https://hub.docker.com/r/sauljabin/kaskade"><img alt="Docker Image Version (latest by date)" src="https://img.shields.io/docker/v/sauljabin/kaskade?label=tag"></a>
<a href="https://hub.docker.com/r/sauljabin/kaskade"><img alt="Docker Image Size (latest by date)" src="https://img.shields.io/docker/image-size/sauljabin/kaskade"></a>

**kaskade** is a [kafka](https://kafka.apache.org/) TUI (text user interface).

:rocket: This project is powered by [textual](https://github.com/willmcgugan/textual)
and [rich](https://github.com/willmcgugan/rich)!.

# Table of Contents

<!-- TOC -->
* [Table of Contents](#table-of-contents)
* [Features](#features)
* [Screenshots](#screenshots)
* [Installation and Usage](#installation-and-usage)
* [Running with Docker](#running-with-docker)
* [Configuration](#configuration)
    * [Kafka](#kafka)
    * [Schema Registry](#schema-registry)
    * [Kaskade](#kaskade)
    * [Other Examples](#other-examples)
* [Alternatives](#alternatives)
* [Development](#development)
    * [Scripts](#scripts)
    * [Kafka Cluster](#kafka-cluster)
    * [Docker](#docker)
    * [Bumping Version](#bumping-version)
<!-- TOC -->

# Features

- List topics, partitions, groups, members
- Topic infor like lag, replicas, record count
- Consume from a topic
- Schema registry support
  - Avro support
- Secure connection

# Screenshots

<p align="center">
<img alt="kaskade" src="https://raw.githubusercontent.com/sauljabin/kaskade/main/screenshots/dashboard.png">
</p>

<p align="center">
<img alt="kaskade" src="https://raw.githubusercontent.com/sauljabin/kaskade/main/screenshots/consumer.png">
</p>

# Installation and Usage

Install with pip:

```shell
pip install kaskade
```

> `pip` will install `kaskade` and `kskd` aliases.

Upgrade with pip:

```shell
pip install --upgrade kaskade
```

Help:

```shell
kaskade --help
```

Version:

```shell
kaskade --version
```

Information, it shows app information:

```shell
kaskade --info
```

Configurations, it shows config examples:

```shell
kaskade --configs
```

Generating a default config yml file:

```shell
kaskade --yml
```

Run without config file (it'll take any of `kaskade.yml`, `kaskade.yaml`, `config.yml` or `config.yaml`):

```shell
kaskade
```

Run with config file:

```shell
kaskade my-config.yml
```

# Running with Docker

Using docker (remember to set a `network` and `volume`):

```shell
docker run --rm -it --network cluster --volume $(pwd):/kaskade sauljabin/kaskade:latest
```

Aliases:

```shell
alias kaskade='docker run --rm -it --network cluster --volume $(pwd):/kaskade sauljabin/kaskade:latest'
alias kskd=kaskade
```

> These aliases will mount the current directory as a volume.

# Configuration

A [yaml](https://yaml.org/spec/1.2/spec.html) configuration file
(check [Installation and Usage](#installation-and-usage) section for more information).

### Kafka

Simple connection example:

```yaml
kafka:
  bootstrap.servers: localhost:9092
```

SSL encryption example:

```yaml
kafka:
  bootstrap.servers: localhost:9092
  security.protocol: SSL
```

> For more information about SSL encryption and SSL authentication go
> to [confluent-kafka](https://github.com/confluentinc/confluent-kafka-python#ssl-certificates)
> and [librdkafka](https://github.com/edenhill/librdkafka/wiki/Using-SSL-with-librdkafka#configure-librdkafka-client).

Support for env variables:

```yaml
kafka:
  bootstrap.servers: ${BOOTSTRAP_SERVERS}
```

### Schema Registry

Simple connection example:

```yaml
schema.registry:
  url: http://localhost:8081
```

### Kaskade

Next settings are optional:

```yaml
kaskade:
  debug: off # enable debug mode, default off
  show.internals: off # show internal topics, default off
```

> `debug` enabled will generate logs into a specific log file, execute `kaskade --info` to get the log path.

### Other Examples

Confluent Cloud:

```yaml
kafka:
  bootstrap.servers: ${BOOTSTRAP_SERVERS}
  security.protocol: SASL_SSL
  sasl.mechanism: PLAIN
  sasl.username: ${CLUSTER_API_KEY}
  sasl.password: ${CLUSTER_API_SECRET}

schema.registry:
  url: ${SCHEMA_REGISTRY_URL}
  basic.auth.user.info: ${SR_API_KEY}:${SR_API_SECRET}
```

# Alternatives

- cli: [[kcat](https://github.com/edenhill/kcat), [zoe](https://github.com/adevinta/zoe), [kaf](https://github.com/birdayz/kaf)]
- wui: [[akhq](https://github.com/tchiotludo/akhq)]
- tui: [[kcli](https://github.com/cswank/kcli)]

# Development

Installing poetry:

```shell
pip install poetry
```

Installing development dependencies:

```shell
poetry install
```

Installing pre-commit hooks:

```shell
poetry run pre-commit install
```

Running kaskade:

```shell
poetry run kaskade
```

### Scripts

Running unit tests:

```shell
poetry run python -m scripts.tests
```

Applying code styles:

```shell
poetry run python -m scripts.styles
```

Running code analysis:

```shell
poetry run python -m scripts.analyze
```

Running code coverage:

```shell
poetry run python -m scripts.coverage
```

Generate readme banner:

```shell
poetry run python -m scripts.banner
```

### Kafka Cluster

Run local cluster:

```shell
cd cluster
docker compose up -d
```

> Open <http://localhost:8080/>

### Docker

Build docker:

```shell
poetry run python -m scripts.docker
```

> Image tag `sauljabin/kaskade:latest`.

Run with docker (create a `config.yml` file):

```shell
docker run --rm -it --network cluster --volume $(pwd):/kaskade sauljabin/kaskade:latest
```

### Bumping Version

Help:

```shell
poetry run python -m scripts.bump --help
```

> More info at https://python-poetry.org/docs/cli/#version and https://semver.org/.

Upgrade (`major.minor.patch`):

```shell
poetry run python -m scripts.bump patch
```
