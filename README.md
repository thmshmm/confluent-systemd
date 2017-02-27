# systemd services for Confluent Platform
Collection of systemd services which can be used to manage kafka, zookeeper, ...

Currently available for:
- Kafka
- ZooKeeper

Up next:
- Confluent Control Center

# Prerequisites
## Log4j settings
Edit /etc/kafka/log4j.properties and change the line
```
log4j.rootLogger=INFO, stdout
```
to
```
log4j.rootLogger=INFO, kafkaAppender
```

## Users, groups and directories
- Create the users and group: kafka, zookeeper
- Create directories: /var/log/kafka, /var/log/zookeeper
- Set appropriate permissions

# Installation
Unit file location: /etc/systemd/system/

Reload systemd:
```
systemd daemon-reload
```

## JMX
JMX is enabled by default. To disable JXM remove the "Environment=" line.

## Kafka
ZooKeeper properties: /etc/kafka/zookeeper.properties

Logs: /var/log/zookeeper

JMX Port: 10030

## ZooKeeper

ZooKeeper properties: /etc/kafka/zookeeper.properties

Logs: /var/log/zookeeper

JMX Port: 10020

