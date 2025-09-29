---
title: kafka basic
date: 2025-09-15 20:40:00 +01:00
categories: [KAFKA]
tags: [kafka]
---

## Kafka - Event-Driven Architectures

- High Throughput
- Fault Tolerance
- Scalability
- Real-Time Processing

### Topic

Where all similar events related to a service can be stored.

- Message Categorization
- Immutable Log
- Multi-Consumer Access
- Decoupled Communication
- Replication

### Broker

- Message Management: Storing, retrieving, distributing messages
- Cluster Node: Each broker is a node in the Kafka cluster
- Scalability: Distributing data across nodes
- Fault Tolerance
- Dynamic Membership: Can join or leave clusters without downtime

### High Availability of Kafka Using Replication

#### Distribution

Distributes a topic's data across multiple brokers in a kafka cluster

#### Parallelism

Enable parallel processing of messages by consumers

#### Scalability

Scale beyond the limitations of a single broker

#### Fault Tolerance

Ensuring data durability

#### Ordering

Stricktly ordered, providing a clear sequence of events

### Serialization

- Json
- Apache Avro
- Protocol Buffers

#### Murmur2 Hash

Ensures even distribution and per-key ordering within a topic's partitions

### Dead Letter Queue

A dead letter queue isolates poison pill messages, enabling analysis and resolution without disrupting the main processing flow.

### CLI Script

```
// download Kafka
wget https://archive.apache.org/dist/kafka/3.0.0/kafka_2.13-3.0.0.tgz

tar -xvf kafka_2.13-3.0.0.tgz

// download Java
sudo yum install java-1.8.0-amazon-corretto

// Generate UUID
bin/kafka-storage.sh random-uuid

// Format Storage
bin/kafka-storage.sh format -t <your-uuid> -c config/kraft/server.properties

// Edit Server Properties
vim config/kraft/server.properties
listeners=PLAINTEXT://0.0.0.0:9092
controller.listeners=PLAINTEXT://0.0.0.0:9093
advertised.listeners=PLAINTEXT://EC2-PRIVATE-IP:9092

// Start Kafka Server
bin/kafka-server-start.sh config/kraft/server.properties

// Create S3 Bucket &
// Upload confluentinc-kafka-connect-s3-10.5.23.zip

// Download and Extract Connector(EC2)
aws s3 cp s3://<your_bucket_name>/confluentinc-kafka-connect-s3-10.5.23.zip .

unzip confluentinc-kafka-connect-s3-10.5.23.zip

// Edit Connect Standalone Properties
vim kafka_2.13-3.0.0/config/connect-standalone.properties

bootstrap.servers=<PRIVATE IP of EC2 instance>:9092
plugin.path=The path where you downloaded the S3 connect
(plugin.path=/home/ec2-user/confluentinc-kafka-connect-s3-10.5.23)

// Create S3 Sink Connector Properties
vim kafka_2.13-3.0.0/config/s3-sink-connector.properties
----------
name=s3-sink-connector
connector.class=io.confluent.connect.s3.S3SinkConnector
tasks.max=1
topics=cartevent
s3.bucket.name=kafka-connect-s3-sink-example
#Replace this with S3 bucket name
s3.region=us-east-1
flush.size=5
rotate.schedule.interval.ms=60000
storage.class=io.confluent.connect.s3.storage.S3Storage
format.class=io.confluent.connect.s3.format.json.JsonFormat
partitioner.class=io.confluent.connect.storage.partitioner.DefaultPartitioner
timezone=UTC
# Converter settings
key.converter=org.apache.kafka.connect.json.JsonConverter
value.converter=org.apache.kafka.connect.json.JsonConverter
key.converter.schemas.enable=false
value.converter.schemas.enable=false
behavior.on.null.values=ignore
----------

// Start Kafka Connect
bin/connect-standalone.sh config/connect-standalone.properties config/s3-sink-connector.properties

```
