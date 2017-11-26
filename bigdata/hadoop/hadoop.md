Hadoop
=======

**Hadoop** is a framework that allows for the distributed processing of large data
 sets across clusters of computers using simple programming models.
 It is designed to scale up from single servers to thousands of machines,
 each offering local computation and storage.
 Rather than rely on hardware to deliver high-availability, the library itself
 is designed to detect and handle failures at the application layer,
 so delivering a highly-available service on top of a cluster of computers,
 each of which may be prone to failures.

The [*Apache Hadoop*](http://hadoop.apache.org/) v2 project includes these modules:

- **Hadoop Common**: The common utilities that support the other Hadoop modules.
- **Hadoop Distributed File System (HDFS)**: A distributed file system that provides
    high-throughput access to application data.
- **Hadoop YARN**: A framework for job scheduling and cluster resource management.
- **Hadoop MapReduce**: A YARN-based system for parallel processing of large data sets.

---

### HDFS - Hadoop Distributed File System

HDFS is the primary distributed storage used by Hadoop applications.
A HDFS cluster primarily consists of a **NameNode** that manages the file system
metadata and **DataNodes** that store the actual data.

The HDFS architecture diagram depicts basic interactions among NameNode,
 the DataNodes, and the clients.
 Clients contact NameNode for file metadata or file modifications and
 perform actual file I/O directly with the DataNodes.

![hdfs_architecture_image](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/images/hdfsarchitecture.png)

 HDFS has a master/slave architecture. An HDFS cluster consists of a single
 NameNode, a master server that manages the file system namespace and regulates
 access to files by clients. In addition, there are a number of DataNodes,
 usually one per node in the cluster, which manage storage attached to the
 nodes that they run on.
 HDFS exposes a file system namespace and allows user data to be stored in files.
 Internally, a file is split into one or more blocks and these blocks are
 stored in a set of DataNodes. The NameNode executes file system namespace
 operations like opening, closing, and renaming files and directories.
 It also determines the mapping of blocks to DataNodes.
 The DataNodes are responsible for serving read and write requests from
 the file system’s clients. The DataNodes also perform block creation,
 deletion, and replication upon instruction from the NameNode.

---

### Hadoop YARN

The fundamental idea of YARN is to split up the functionalities of
 resource management and job scheduling/monitoring into separate daemons.
 The idea is to have a global ResourceManager (RM) and per-application
 ApplicationMaster (AM).
 An application is either a single job or a DAG of jobs.
 
 ![yarn_architecture image](http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/yarn_architecture.gif)

 The ResourceManager is the ultimate authority that arbitrates
 resources among all the applications in the system.
 The NodeManager is the per-machine framework agent who is responsible
 for containers, monitoring their resource usage (cpu, memory, disk, network)
 and reporting the same to the ResourceManager/Scheduler.

The per-application ApplicationMaster is, in effect, a framework specific
 library and is tasked with negotiating resources from the ResourceManager
 and working with the NodeManager(s) to execute and monitor the tasks.
 
 
 
---

*MapReduce in hadoop-2.x maintains API compatibility with
previous stable release (hadoop-1.x).
This means that all MapReduce jobs should still run unchanged
on top of YARN with just a recompile.*


---

### References:
1. [Apache™ Hadoop®](http://hadoop.apache.org/)
2. [Hadoop v1 Commands](https://github.com/animenon/Tech-FAQs/blob/master/bigdata/hadoop/hdfs_v1_commands.md)
3. [Hadoop v2 Commands](https://github.com/animenon/Tech-FAQs/blob/master/bigdata/hadoop/hdfs_v2_commands.md)
