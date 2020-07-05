# Distributed Data Flow Systems

### Streaming Data Framework features

- Message Delivery Semantics
- State Management
- Fault Tolerance


Data delivery semantics maybe -

- At least once
- At most once
- Exactly once


Systems may maintain state in-memory or in persistent storage.

Systems maybe stateful or state-less.

Systems maybe fault tolerant to the below points of failure-
1. Incoming Stream failure
2. Network failure (between source and processing system)
3. Stream Processing failure
4. Connection to Sink failure
5. Output Sink/destination system failure
6. Streaming manager failure (Processing System specific)
7. Application Driver failure (Processing System specific)

Approaches for better fault tolerance in systems -

1.  Replication and Coordination
  - Replicate the state of computation on multiple nodes
  - In case of failure, streaming manager interacts with replicas to continue
  - Predefine number of simultaneous failures for better handling system wide failures without data loss.
    (K-fault tolerent systems, can tolerate 'k' failures)
2. State machine approach
  - Streaming job is replicated on multiple nodes
  - Replicas are coordinated by sending same input in same order to all
  - Allows for quick failover, resulting into little disruption
3. Rollback recovery approach
  - Stream processor periodically packages the state of computation into checkpoint
  - Copies checkpoint to different nodes
  - In case of failure, stream manager fetches the computation from last saved checkpoint and reschedules it.


### Features of a Streaming platform

- Publish and subscribe to streams of records
- Store streams of records in a fault-tolerant durable way
- Process streams of records as they arrive

## Data Flow/Ingestion systems

- Apache Kafka - High-Throughput Distributed Messaging System.
- Apache Flume
- 

### Stream Processing systems -

- Apache Flink
- Apache Storm
- Apache Spark (Streaming)
- Apache Samza

## Terminology

A stream is an unbounded, continuously updating data set. A stream is an ordered, replayable, and fault-tolerant sequence
 of immutable data records, where a data record is defined as a key-value pair.

A stream processing application defines its computational logic through one or more processor topologies, where a
 processor topology is a graph of stream processors (nodes) that are connected by streams (edges).

A stream processor is a node in the processor topology; it represents a processing step to transform data in streams by
 receiving one input record at a time from its upstream processors in the topology, applying its operation to it, and
 may subsequently produce one or more output records to its downstream processors.

### Timimg in Streams

- Event Time - Time at which the event occurs
- Stream Time - Time at which the event enters the streaming system

    Time Skew <- Stream Time - Event Time

### Windowing in streams

Windowing is a necesity in stream processing as data flows infinitly(until system is alive) into the system and the whole
 data can't be stored in-memory (or be processed in real-time).

Windowing can be implemented time-based or count-based.
- Time-based - Data older than a threshold will be evicted to make space for newer records.
- Count-based - Data/Events which are older than a certain count will be evicted.

**Types of Windowing**

- Sliding Window - tuples are grouped within a window that slides across the data stream according to a specified interval.

  ![Sliding Window HortonWorks Image](https://docs.cloudera.com/HDPDocuments/HDP2/HDP-2.6.5/bk_storm-component-guide/content/figures/4/figures/sliding-window.png)

- Tumbling Window - tuples are grouped in a single window based on time or count. A tuple belongs to only one window.

  ![Tumbling Window Hortonworks Image](https://docs.cloudera.com/HDPDocuments/HDP2/HDP-2.6.5/bk_storm-component-guide/content/figures/4/figures/tumbling-window.png)

  - Count-based Tumbling Window - A type of tumbling window where trigger policy is count based and eviction is as the
     window is full.

  - Temporal Tumbling Window - A type of tumbling window where there is no constraints in number of tuples in window
     but window is drained once eviction time is reached.


