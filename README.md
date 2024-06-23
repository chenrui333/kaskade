<p align="center">
<a href="https://github.com/sauljabin/kaskade"><img alt="kaskade" src="https://raw.githubusercontent.com/sauljabin/kaskade/v2/images/banner.png"></a>
</p>
<a href="https://github.com/sauljabin/kaskade"><img alt="GitHub" height="20" src="https://img.shields.io/badge/-github-blueviolet?logo=github&logoColor=white"></a>
<a href="https://github.com/sauljabin/kaskade/blob/main/LICENSE"><img alt="MIT License" src="https://img.shields.io/github/license/sauljabin/kaskade"></a>
<a href="https://pypi.org/project/kaskade"><img alt="Version" src="https://img.shields.io/pypi/v/kaskade?label=latest"></a>
<a href="https://pypi.org/project/kaskade"><img alt="Python Versions" src="https://img.shields.io/pypi/pyversions/kaskade?label=python"></a>
<a href="https://pypi.org/project/kaskade"><img alt="Platform" src="https://img.shields.io/badge/os-linux%20%7C%20macos-blue"></a>

## Kaskade

Kaskade is a text user interface (TUI) for Apache Kafka, built with [Textual](https://github.com/Textualize/textual).
It includes features like:

- List topics, partitions, groups, members
- Topic information like lag, replicas, records count
- Consume from a topic
- Schema registry support
- String, Avro, Json and Protobuf deserialization
- Secure connection

<p align="center">
<img alt="kaskade" src="https://raw.githubusercontent.com/sauljabin/kaskade/main/screenshots/dashboard.png">
</p>

## Installation

Install with `pipx`:

```shell
pipx install kaskade
```

> `pipx` will install `kaskade` and `kskd` aliases.

Upgrade with `pipx`:

```shell
pipx upgrade kaskade
```

<a href="https://hub.docker.com/r/sauljabin/kaskade"><img alt="docker image available" height="20" src="https://img.shields.io/badge/-docker image available-blue?logo=docker&logoColor=white"></a>

## Running Kaskade

Pass the option `-b` (boostrap servers):

```shell
kaskade -b localhost:9092
```

Help:

```shell
kaskade --help
```

## Configuration Examples

### SSL encryption example:

```shell
kaskade -b localhost:9092 -x security.protocol=SSL
```

For more information about SSL encryption and SSL authentication go
to the `librdkafka` official page: [Configure librdkafka client](https://github.com/edenhill/librdkafka/wiki/Using-SSL-with-librdkafka#configure-librdkafka-client).

### Multiple bootstrap servers:

```shell
kaskade -b broker1:9092,broker2:9092
```

### Schema Registry simple connection:

```shell
kaskade -b localhost:9092 -s url=http://localhost:8081
```

More Schema Registry configurations at: [confluent-kafka-python documentation](https://docs.confluent.io/platform/current/clients/confluent-kafka-python/html/index.html#schemaregistry-client).

### Confluent Cloud:

```shell
kaskade -b ${BOOTSTRAP_SERVERS} \
        -x security.protocol=SASL_SSL \
        -x sasl.mechanism=PLAIN \
        -x sasl.username=${CLUSTER_API_KEY} \
        -x sasl.password=${CLUSTER_API_SECRET} \
        -s url=${SCHEMA_REGISTRY_URL} \
        -s basic.auth.user.info=${SR_API_KEY}:${SR_API_SECRET}
```

## Development

For development instructions see [DEVELOPMENT.md](DEVELOPMENT.md).