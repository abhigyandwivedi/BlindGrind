# Apache Kafka - Key Terminologies

## 🔑 Core Kafka Terminologies

|Term|Explanation|
|---|---|
|**Kafka**|A distributed streaming platform that lets you publish, subscribe to, store, and process data streams in real-time.|
|**Broker**|A Kafka server that stores data and serves client requests. A Kafka cluster consists of one or more brokers.|
|**Topic**|A logical channel to which data (messages) are written and read. Think of it as a feed or stream name.|
|**Partition**|A topic is split into partitions for scalability and parallelism. Each partition is an ordered, immutable sequence of records.|
|**Offset**|A unique identifier for each message in a partition. It acts as a position marker that consumers use to track their reading progress.|
|**Producer**|A client that publishes (writes) data to Kafka topics.|
|**Consumer**|A client that subscribes to Kafka topics and processes incoming data.|
|**Consumer Group**|A group of consumers working together to consume data from a topic. Kafka ensures each partition is read by only one consumer within a group.|
|**Replication Factor**|The number of copies of a partition across different brokers for fault tolerance.|
|**Leader**|For each partition, one broker is elected as the leader. All reads/writes go through the leader.|
|**Follower**|Other brokers that replicate the leader’s partition. They sync data from the leader.|
|**ZooKeeper**|Previously used to manage metadata and broker coordination in Kafka. Modern Kafka uses **KRaft** mode (Kafka Raft) instead of ZooKeeper.|
|**KRaft**|Kafka’s own consensus protocol replacing ZooKeeper in newer versions.|
|**Retention**|The amount of time Kafka keeps a message in a topic, even after it has been read by consumers.|
|**Log**|A partition is essentially a **commit log** where messages are appended in order.|
|**Lag**|The difference between the last offset produced and the last offset consumed. It indicates how far behind the consumer is.|

## 🔄 Message/Record Structure

|Term|Explanation|
|---|---|
|**Message** / **Record**|The unit of data in Kafka. It consists of a **key**, **value**, **timestamp**, and **offset**.|
|**Key**|Determines the partition to which the message goes (when using partitioning by key).|
|**Value**|The actual data/payload being sent.|
|**Timestamp**|The time when the message was produced or logged.|

## ⚙️ Other Concepts

| Term                                    | Explanation                                                                                        |
| --------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **Retention Policy**                    | Defines how long Kafka stores messages (based on time or size).                                    |
| **Compaction**                          | A cleanup policy that keeps only the latest record per key in a topic.                             |
| **Throughput**                          | The volume of data Kafka can handle per unit time.                                                 |
| **Serialization** / **Deserialization** | Converts data to/from byte format when writing to/reading from Kafka (e.g., JSON, Avro, Protobuf). |
| **Kafka Streams**                       | A client library for building stream processing applications on top of Kafka.                      |
| **Connect (Kafka Connect)**             | A tool for integrating Kafka with external systems (e.g., databases, file systems).                |

#kafka