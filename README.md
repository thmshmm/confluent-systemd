# systemd services for Confluent Platform

Collection of systemd services which can be used to manage kafka, zookeeper, ...

Currently available for:
- ZooKeeper

Up next:
- Kafka

# Installation
Unit file location: /etc/systemd/system/

Reload systemd:
```
systemd daemon-reload
```

# ZooKeeper

ZooKeeper properties: /etc/kafka/zookeeper.properties
Log: /var/log/zookeeper/zookeeper.out

JMX Port: 10020
JMX is enabled by default. To disable JXM remove the "Environment=" line.

The service routes all standard output into the specified log.

