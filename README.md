# Docker Kafka MirrorMaker
Docker container that runs Kafka's MirrorMaker.

Kafka Version: 0.8.2.1

## Usage
[The MirrorMaker documentation says](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330):

> Setting up a mirror is easy - simply start up the mirror-maker processes after bringing up the target cluster. At minimum, the mirror maker takes one or more consumer configurations, a producer configuration and either a whitelist or a blacklist. You need to point the consumer to the source cluster's ZooKeeper, and the producer to the mirror cluster's ZooKeeper (or use the broker.list parameter).



The container expects the following environment variables to be passed in:

* `CONSUMER_ZK_CONNECT` - Zookeeper connection string for source, including port and chroot.
* `DOWNSTREAM_BROKERS` - Brokers to receive mirrored messages
* `WHITE_LIST` - (optional) White list of topics, if used, do not use black list
* `BLACK_LIST` - (optional) Black list of topics, if used, do not use white list
* `CONSUMER_GROUP_ID` - (optional) Defaults to 1
* `PRODUCER_COUNT` - (optional) Defaults to 1
* `STREAM_COUNT` - (optional) Defaults to 1

<!-- * `ABORT_ON_FAILURE` - (optional) Kill MirrorMaker on failure. Defaults to true.
* `OFFSET_COMMIT_INTERVAL` - (optional) Defaults to 60000 -->

### Command
`docker run -e WHITE_LIST="topic" -e CONSUMER_ZK_CONNECT=localhost:2181/chroot -e DOWNSTREAM_BROKERS=127.0.0.1:9092 sheeley/docker-kafka-mirrormaker`

## Building
`docker build -t sheeley/docker-kafka-mirrormaker .`

## Limitations
- Currently only supports a single consumer
- Does not support message handlers
- Does not support rebalancers 

## MirrorMaker Documentation
https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330
