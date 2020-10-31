![HDFS](https://hadoop.apache.org/docs/r2.7.1/hadoop-project-dist/hadoop-hdfs/images/hdfs-logo.jpg)
=============================


**Hadoop Distributed File System**

HDFS is a distributed file system designed to run on commodity hardware.
 HDFS is highly fault-tolerant and is designed to be deployed on low-cost hardware.
 HDFS provides high throughput access to application data and is suitable for applications that have large data sets.
 HDFS relaxes a few POSIX requirements to enable streaming access to file system data.

HDFS was originally built as infrastructure for the Apache Nutch web search engine project.


HDFS is designed to overcome some of the common issues in distributed file systems like:
Hardware Failure, Streaming Data Access(high throughput of data access rather than low latency of data access), 
Portability Across Heterogeneous Hardware and Software Platforms.

It works on “Moving Computation is Cheaper than Moving Data”.

![HDFS Architecture](https://hadoop.apache.org/docs/r1.2.1/images/hdfsarchitecture.gif)

HDFS has a master/slave architecture.
 An HDFS cluster consists of a single NameNode, a master server that manages the file system namespace and regulates access to files by clients.
 And many DataNodes(usually one per node in the cluster) which manage storage attached to the nodes that they run on.

A file on HDFS is split into one or more blocks and these blocks are stored in a set of DataNodes.

**NameNode** executes file system namespace operations like opening, closing, and renaming files and directories. It also determines the mapping of blocks to DataNodes.

**DataNodes** are responsible for serving read and write requests from the file system’s clients.
 It also perform block creation, deletion, and replication upon instruction from the NameNode.

NameNode and DataNode are software components written to run on JVM(java virtual machine), hence making it easily portable and deploy-able on various systems.

NameNode is the arbitrator and repository for all HDFS metadata. The system is designed in such a way that user data never flows through the NameNode. 

Read More: [HDFS Architecture Guide](https://hadoop.apache.org/docs/r1.2.1/hdfs_design.html) 