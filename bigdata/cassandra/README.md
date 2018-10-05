## CASSANDRA

> “Apache Cassandra is an open source, distributed, decentralized, elastically scalable,
> highly available, fault-tolerant, tuneably consistent, row-oriented database that bases
> its distribution design on Amazon’s Dynamo and its data model on Google’s Bigtable.
> Created at Facebook, it is now used at some of the most popular sites on the Web.”
>
> \- Cassandra: The Definitive Guide (book)

### FEATURES

- **Distributed and Decentralized**: Cassandra is capable of running on multiple
machines while appearing to users as a unified whole without any SPOF(single point of failure).
- **Elastic Scalability**: Easy horizontal scaling (i.e. cluster can seamlessly scale up
and scale back down.)
- **High Availability and Fault Tolerance**: Cassandra is highly available as data maybe replicated over multiple datacenters.
- **Tuneable Consistency**: Eventual/Causual/Strict consistency maybe set by tuning replication factor
 and consistency level(how many replicas in the cluster must acknowledge a write operation
 or respond to a read operation in order to be considered successful).
