# systemd services for Confluent Platform
Collection of systemd services which can be used to manage kafka, zookeeper, ...

Currently available for:
- Kafka
- Kafka Connect
- ZooKeeper

Up next:
- Confluent Control Center

# Prerequisites
## Kafka/ZooKeeper Log4j settings
Edit /etc/kafka/log4j.properties, add/change the following line
```
log4j.rootLogger=INFO, kafkaAppender
```

## Kafka Connect Log4j settings
Edit /etc/kafka/connect-log4j.properties, add/change the following lines
```
log4j.rootLogger=INFO, kafkaConnectAppender

log4j.appender.kafkaConnectAppender=org.apache.log4j.DailyRollingFileAppender
log4j.appender.kafkaConnectAppender.DatePattern='.'yyyy-MM-dd-HH
log4j.appender.kafkaConnectAppender.File=${kafka.logs.dir}/connect.log
log4j.appender.kafkaConnectAppender.layout=org.apache.log4j.PatternLayout
log4j.appender.kafkaConnectAppender.layout.ConversionPattern=[%d] %p %m (%c)%n
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
Kafka properties: /etc/kafka/server.properties

Logs: /var/log/kafka

JMX Port: 10030

## Kafka Connect
Kafka Connect properties: /etc/kafka/connect-distributed.properties

Log: /var/log/kafka/connect.log

JMX Port: 10040

## ZooKeeper

ZooKeeper properties: /etc/kafka/zookeeper.properties

Logs: /var/log/zookeeper

JMX Port: 10020

