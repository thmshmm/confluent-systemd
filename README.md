# systemd services for Confluent Platform

Available for:
- Confluent Kafka
- Confluent Schema Registry
- Confluent Kafka Connect
- Confluent ZooKeeper
- Confluent Control Center

## Prerequisites

### Users, groups and directories
- Create the users and group:
  - kafka
  - zookeeper
  - confluent-cc
- Create directories:
  - /var/log/kafka
  - /var/log/zookeeper
  - /var/log/confluent-control-center
- Set appropriate permissions

### Kafka Connect Log4j settings
Edit /etc/kafka/connect-log4j.properties, add/change the following lines
```
log4j.rootLogger=INFO, kafkaConnectAppender

log4j.appender.kafkaConnectAppender=org.apache.log4j.DailyRollingFileAppender
log4j.appender.kafkaConnectAppender.DatePattern='.'yyyy-MM-dd-HH
log4j.appender.kafkaConnectAppender.File=${kafka.logs.dir}/connect.log
log4j.appender.kafkaConnectAppender.layout=org.apache.log4j.PatternLayout
log4j.appender.kafkaConnectAppender.layout.ConversionPattern=[%d] %p %m (%c)%n
```

### Confluent Control Center
For logging into files, rename log4j-rolling.properties to log4j.properties. </br>
By default Control Center will log to /tmp. To change, set the paths in log4j.properties after renaming.

# Installation
Put the unit file into the location: /etc/systemd/system/ </br>
Reload systemd:
```
systemctl daemon-reload
```

For auto restart of these services use:
```
systemctl enable servicename.service
```
# Summary
JMX is enabled by default. To disable JXM remove the "Environment=" line.

## Confluent Kafka
Kafka properties: /etc/kafka/server.properties </br>
Logs: /var/log/kafka </br>
JMX Port: 10030

## Confluent Schema Registry
Schema Registry properties: /etc/schema-registry/schema-registry.properties </br>
JMX Port: 10050

## Confluent Kafka Connect
Kafka Connect properties: /etc/kafka/connect-distributed.properties </br>
Log: /var/log/kafka/connect.log           </br>
JMX Port: 10040

## Confluent ZooKeeper
ZooKeeper properties: /etc/kafka/zookeeper.properties </br>
Logs: /var/log/zookeeper                              </br>
JMX Port: 10020                                       </br>
