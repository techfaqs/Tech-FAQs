
# Apache kafka

Apache Kafka is a distributed streaming platform.

#### A streaming platform has three key capabilities:

- Publish and subscribe to streams of records, similar to a message queue or enterprise messaging system.
- Store streams of records in a fault-tolerant durable way.
- Process streams of records as they occur.

#### Kafka is generally used for two broad classes of applications:

- Building real-time streaming data pipelines that reliably get data between systems or applications
- Building real-time streaming applications that transform or react to the streams of data

## Installation

1. Download the code from: [here](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.5.0/kafka_2.12-2.5.0.tgz)
2. Un-tar the downloaded tar and and change directory into it:

       > tar -xzf kafka_2.12-2.5.0.tgz
       > cd kafka_2.12-2.5.0
_(add the kafka directory path as `KAFKA_HOME` or you will have to use the absolute path to use it)_

3. For Linux, change directory into `bin/` and you may execute kafka commands from here.. 
   
   Or
   
   For Windows, change directory into `bin\windows` and you may execute kafka commands from here.. 
   
4. You will require to setup various configuration of kafka/zookeper in `config` directory (in `KAFKA_HOME` location).

Have a look at [Kafka Quickstart](https://kafka.apache.org/quickstart) for further steps..
   
## Example

For a sample run follow: [Console Example](https://github.com/techfaqs/Tech-FAQs/blob/master/bigdata/kafka/console-example.md)

Reference: [Apache Kafka Intro](https://kafka.apache.org/intro.html)

### Internals of Kafka -

- Topic - a physical partitioning of the data such that all data contained within the topic should be somehow related
 such that they can be parsed by the same common mechanism and not much else.
- Partition - ordered, immutable sequence of records that is continually appended to a structured commit log.
  The records in the partitions are each assigned a sequential id number called the offset that uniquely identifies each
   record within the partition.
- Broker - Partitions themselves are distributed among brokers, which are the physical processes that make up a Kafka cluster.
   Typically, each broker in the cluster corresponds to a separate physical server and manages all of the writes to
   that server's disk. The partitions are then uniformly distributed across the different brokers.
- Producer - used to write data into topics
- Consumer - used to read data from topics


---

#### Log-Structured Storage

Kafka is structured around an append-only log mechanism similar to the write-ahead-log protocol found in database applications.
That is before an object can be mutated, the log of its mutation must first have been committed to a recovery log, this
 forms an “undo” log of message mutations that can be applied or removed from the database to reconstruct the state of
 the database at any particular moment in time.

#### Retention

Kafka uses time-based retention mechanism for its logs. Logs are moved after certain hours of retention(usually defaults
 to a week i.e. 168 hours). Set using the `log.retention.hours` config, when a log segment exceeds this age it is deleted
 (on a per-partition basis). There is also `log.retention.bytes` which could be set to a 32 bit integer, but that limits
 partition size to 2GB/partition per topic.

The size of each segment is controlled by the `log.segment.bytes`(size of log segment i.e. size of file containing actual
 message sent to kafka) and the `log.index.size.max.bytes`(the size of the index file that accompanies each log segment)
 settings. Index file is used to store index information about the offsets for each message stored in the file.
 It is allocated 10MB of space using a sparse file method by default, but if it fills up before the segment file itself
 is filled, it causes a new log segment to roll over.
The rate at which segments are checked for expiration is controlled by `log.cleanup.interval.mins` (defaults to `1`).


#### Not a queuing system

Its not a queuing syatem like ActiveMQ or RabbitMQ, which go through a lot of trouble to ensure that messages are processed
 in the order that they were received. Also the messages are not removed from the system once they are consumed and relies on
 consumers to keep track of the offset of message read, this is simplified as the offsets would be inturn managed by Zoo Kepper.

#### Replication

Replication is handled at a topic level. Each partition of a topic has a leader partition that is replicated by zero or
 more follower partitions. These follower partitions are distributed among the different physical brokers with the
 intent to place each follower on a different broker. Implementations should ensure that they have sufficient broker
 capacity to support the number of partitions and replicas that will be used for a topic.
When a partition is created, all of its followers are considered to be “in-sync” and form the in-sync replica set (ISR).
 When a message arrives at the leader partition to be written, it is first appended to the leader's log. And then
 forwarded to each of the follower partitions currently in the ISR. After each of the partitions in the ISR acknowledges
 the message, the message is considered to be committed and can now be read by consumers.

#### Handling failures

If a broker containing a particular replica fails, it is removed from the ISR and the leader does not wait for its
 response. This is handled through Kafka's use of ZooKeepers to maintain a set of “live” brokers. The leader then
 continues to process messages using the smaller pool of replicas in the ISR. When the replica recovers, it examines
 its last-known high watermark and truncates its log to that partition. The replica then copies data from this position
 to the current committed offset of the leader. After the replica has caught up, it may be added back to the ISR and
 everything proceeds as before.

Kafka Producer API has three levels of acknowledgment available -

- `none` - no response is sent to the producer after message is written to kafka socket. High performance but messages may be lost.
- `leader` - response/acknowledgement is sent as the leader receives the message. Might lead to data loss but better
   durable than the previous approach.
- `all` - Acknoledgement is only sent after the leader has committed the message (all in-sync replicas have written the message).
   Chances of data loss are grim as data will be available as long as at least one replica still exits.

#### Multiple datacenter deployments (required in global/geo-distributed setup)

Kafka's mirroring feature makes it possible to maintain a replica of an existing Kafka cluster by using **MirrorMaker**
 tool to mirror a source Kafka cluster into a target (mirror) Kafka cluster.

[More on MirrorMaker here](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330)



![]()

[//]: # (A UML linking all these components:
![UML linking Kafka components](https://insidebigdata.com/wp-content/uploads/2018/04/Instaclustr_fig1.png
Image from https://insidebigdata.com/)

Refer: [Apache Kafka Intro](https://kafka.apache.org/intro)
