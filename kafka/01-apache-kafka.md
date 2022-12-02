# What Is Kafka
#kafka

Apache Kafka is an open-source distributed event streaming platform used by thousands of companies for high-performance data pipelines, streaming analytics, data integration, and mission-critical applications.

## What is event streaming?
#event_streaming

Event streaming is the practice of capturing data in real-time from event sources like databases, sensors, mobile devices, cloud services, and software applications in the form of streams of events; storing these event streams durably for later retrieval; manipulating, processing, and reacting to the event streams in real-time as well as retrospectively; and routing the event streams to different destination technologies as needed. Event streaming thus ensures a continuous flow and interpretation of data so that the right information is at the right place, at the right time.

## Kafka Topics
#kafka_topics
- Topics are particular stream of data, there can be multiple topics in a Kafka cluster with different names.
- In comparison Kafka topic can be considered as a table in a database but without any constraint. We can send any type of data to a topic, Json, Avro, xml.
- We can have as many topics as per our desire in a Kafka cluster.
- A topic is identified by its name.
- Kafka topics supports any kind of message format Json, text, binary.

**Data Stream:** The sequence of messages in a topic is called a data stream. #data_stream
- Kafka topics cannot be queried
	- To Send data to topic use Kafka producers.
	- To read data from topics Use Kafka Consumers.

## Partitions and Offsets
#partitions
- Topics are split into partitions, (eg: 100 partitions)
	- Messages are send to partitions 
	- Messages in each partitions are ordered
	- Each message within a partitions gets an incremental id, also know as offset. #kafka_offset

- Kafka topics are **immutable**: once written to a partition, it cannot be changed.
- We cannot delete or update data in Kafka
- We have to keep on writing to partitions

![[Kafka-Topics-and-Patitions-1024x310.webp]]

### Summary:

- Once data written to partition cannot be changed (Immutability)
- Data is kept only for a limited time (Default is one week - this is configurable)
- Offset has only meaning for each partition.
	- Eg: Offset 3 in partition 0 does not represent same data as offset 3 partition 1 data
	- Offsets are not re-used even if previous messages have been deleted.
- Order is guaranteed only with in a partition (not across partitions)
- Data is assigned randomly to a partition unless a key is provided.
- You can have as many partitions per topic as you want.
