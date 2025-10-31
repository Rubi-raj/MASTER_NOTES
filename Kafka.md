# **![][image1]**

# **What is Kafka ?**

 Apache Kafka is a **distributed streaming platform** used for building real-time data pipelines and applications, acting as a high-throughput, low-latency platform for handling real-time data feeds.

What is DLT ?  
 DLT stands for Dead Letter Topic, means If a message is not able to consume by consumer it send to DLT.

**Simple:-**

| Producer | Publish a Message/Events |
| :---- | :---- |
| **Consumer** | Consuming a Message/Events |
| **Broker** | Distributed System (Available in multiple servers) |
| **Cluster** | Kafka Server |
| **Topic** | Like Queue |
| **Partitions** | Spliting a Topic into multiple Partitions. |
| **Offset** | Index of the Messages called Offset number. |
| **Consumer Groups** | Grouping the Consumers. |
| **Zookeeper** | Managing a Kafka |

**Elaborated:-**

| Producer | An application that publishes data (messages) to Kafka topics. It optimizes, serializes, and balances messages across partitions. |
| :---- | :---- |
| **Consumer** | An application that subscribes to Kafka topics and reads messages from partitions, typically within a consumer group. |
| **Broker** | A Kafka server that manages message storage and handles read/write requests. Brokers work together to form a Kafka cluster. |
| **Topic** | A logical channel that organizes messages. Producers write to topics, and consumers subscribe to them. |
| **Partition** | A sub-division of a topic that enables parallel processing. Each partition is replicated across brokers for fault tolerance. |
| **ZooKeeper / KRaft** | Coordinates and manages Kafka brokers and clusters, ensuring fault tolerance and leader elections for partitions. |
| **Replication** | Ensures copies of partitions are maintained across different brokers to enhance fault tolerance and availability. |
| **Consumer Group** | A group of consumers sharing the workload of processing messages from partitions of a topic, ensuring parallelism. |
| **Leader** | The broker responsible for handling all reads and writes for a partition. Each partition has one leader at any time. |
| **Follower** | Brokers that replicate data from the leader broker for redundancy and failover purposes. |

[image1]: <data:image/png;base64,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>