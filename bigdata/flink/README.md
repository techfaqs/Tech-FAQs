# Apache Flink

Apache Flink is a framework and distributed processing engine for stateful computations over
 unbounded and bounded data streams.
Flink has been designed to run in all common cluster environments, perform computations at
 in-memory speed and at any scale.

All data is processed as streams in Flink. It can be **Unbounded streams**(have a start but no defined end)
 or **Bounded streams**(a.k.a *batch processing*, have a defined start and end).

> Processing unbounded data often requires that events are ingested in a specific order,
>  such as the order in which events occurred, to be able to reason about result completeness.
> Ordered ingestion is not required to process bounded streams because a bounded data set can always be sorted.

Flink integrates with all common cluster resource managers such as
**Hadoop YARN, Apache Mesos**, and **Kubernetes** but can also be setup to run as a **stand-alone cluster**.

Flink easily maintains very large application state. Its asynchronous and incremental checkpointing algorithm
 ensures minimal impact on processing latencies while guaranteeing exactly-once state consistency.

Stateful Flink applications are optimized for local state access. Task state is always maintained in memory or,
if the state size exceeds the available memory, in access-efficient on-disk data structures.
Hence, *tasks perform all computations by accessing local, often in-memory, state yielding very low processing latencies*.
![In-Memory Performance](https://flink.apache.org/img/local-state.png)

> Flink guarantees exactly-once state consistency in case of failures by periodically and asynchronously
> checkpointing the local state to durable storage.

---

## Building blocks of Flink

#### Streams

- **Bounded and unbounded streams** - Flink has sophisticated features to process unbounded streams and
 dedicated operators to efficiently process bounded streams
- **Real-time and recorded streams** - Data can either be processed in real-time as it is generated or
   persisted to a storage system(e.g., a file system or object store), and processed later.

#### State

Every non-trivial streaming application is stateful, i.e., only applications that apply transformations
 on individual events do not require state. Flink provides in the context of state handling.

- **Multiple State Primitives**: Flink provides state primitives for different data structures, such as atomic values, lists, or maps.
- **Pluggable State Backends**: Application state is managed in and checkpointed by a pluggable state backend.
   Flink features different state backends that store state in memory or in RocksDB, an efficient embedded on-disk data store.
   Custom state backends can be plugged in as well.
- **Exactly-once state consistency*: Flink’s checkpointing and recovery algorithms guarantee the consistency of application state in case of a failure. Hence, failures are transparently handled and do not affect the correctness of an application.
- **Very Large State**: Flink is able to maintain application state of several terabytes in size due to its asynchronous and incremental checkpoint algorithm.
- **Scalable Applications**: Flink supports scaling of stateful applications by redistributing the state to more or fewer workers.


#### Time

 Most event streams have inherent time semantics because each event is produced at a specific point in time.
Moreover, many common stream computations are based on time, such as windows aggregations, sessionization, pattern detection, and time-based joins.

Flink's rich set of time-related features -

- Event-time Mode: Event-time processing allows for accurate and consistent results regardless whether recorded or real-time events are processed.
- Watermark Support: flexible mechanism to trade-off the latency and completeness of results.
- Late Data Handling: Flink features multiple options to handle late events, such as rerouting them via side outputs and updating previously completed results.
- Processing-time Mode: Flink also supports processing-time semantics which performs computations as triggered by
 the wall-clock time of the processing machine. The processing-time mode can be suitable for certain applications with strict low-latency requirements that can tolerate approximate results.


### Layered APIs

![Flink Layered APIs](https://flink.apache.org/img/api-stack.png)


Flink features several **libraries** for common data processing use cases, like -

- Complex Event Processing (CEP): Flink’s CEP library provides an API to specify patterns of events (think of regular expressions or state machines). The CEP library is integrated with Flink’s DataStream API, such that patterns are evaluated on DataStreams. Applications for the CEP library include network intrusion detection, business process monitoring, and fraud detection.

- DataSet API: The DataSet API is Flink’s core API for batch processing applications. The primitives of the DataSet API include map, reduce, (outer) join, co-group, and iterate. All operations are backed by algorithms and data structures that operate on serialized data in memory and spill to disk if the data size exceed the memory budget. The data processing algorithms of Flink’s DataSet API are inspired by traditional database operators, such as hybrid hash-join or external merge-sort.

- Gelly: Gelly is a library for scalable graph processing and analysis. Gelly is implemented on top of and integrated with the DataSet API. Hence, it benefits from its scalable and robust operators. Gelly features built-in algorithms, such as label propagation, triangle enumeration, and page rank, but provides also a Graph API that eases the implementation of custom graph algorithms.

Apache Flink is a framework for stateful computations over unbounded and bounded data streams. Since many streaming
 applications are designed to run continuously with minimal downtime, a stream processor must provide excellent
 failure recovery, as well as, tooling to monitor and maintain applications while they are running.

Consistency is maintained with-
- Consistent Checkpoints

- Efficient Checkpoints

- End-to-End Exactly-Once

- Integration with Cluster Managers

- High-Availability Setup

Reference: [Apache Flink](https://flink.apache.org/)
