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

> Application's measure of time is the difference of event-time and processing-time






Reference: [Apache Flink](https://flink.apache.org/)
