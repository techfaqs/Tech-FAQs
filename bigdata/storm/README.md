# Storm

Storm is a stream-processing framework developed by BackType, which was a marketing analytics company that was analyzing
 Twitter data. BackType was later acquired by Twitter ans Storm was open-sourced.
Storm is a distributed realtime computation system. It is scalable and fault-tolerant system that has many use cases like:
 realtime analytics, online machine learning, continuous computation, distributed RPC, ETL, etc.

Storm build applications as DAGs(directed acyclic graphs) called Topologies. The top of the graph is a data source
(maybe kafka or any other), these data sources are called **spouts**. They then pass the data onto units of computation
 called **bolts**.

There are higher abstract leyers on top of this which facilitate easier use like:
- Trident - provides exactly-once processing, "transactional" datastore persistence, and a set of common stream analytics operations.
- Stream APIs - provides a typed API for expressing streaming computations and supports functional style operations.
- Storm SQL(experimental) - allows users to run SQL queries over streaming data in Storm.


## Components of a Storm CLuster

#### ZooKeeper

A distributed Storm cluster relies on ZooKeeper for coordinating the cluster. Used to manage metadata.
ZooKeeper keeps track of all running topologies as well as the status of all supervisors.

#### Nimbus

It is responsible for the distribution of individual tasks for either spouts or bolts across the workers in the cluster.
 It is also responsible for rebalancing a Storm cluster in the event a supervisor has crashed. 
If the nimbus goes down, existing topologies continue to function unimpeded. The Nimbus is not involved in the moment-to-moment 
 processing—just the distribution of processing tasks to the supervisor nodes.
When the nimbus crashes, the cluster is no longer able to manage topologies. Hence it needs to be restarted quickly.

#### Supervisors

Supervisors are servers that run on each of the worker nodes and manage the execution of local tasks. Each of the local
 tasks is either a spout or a bolt, and there can be many local tasks running under the control of each supervisor.

If a supervisor goes down, all tasks under it are lost and Nimbus restarts them with a supervisor again.
When a new supervisor is added the existing topologies are not automatically rebalanced, `rebalance` needs to be run.


## Storm Topologies

Storm topologies are run in a Storm cluster by the following 3 entities - 
- Worker processes
- Executors (threads)
- Tasks

![illustration of three main entities running storm cluster](https://storm.apache.org/releases/2.2.0/images/relationships-worker-processes-executors-tasks.png)

**Configuring the parallelism of a topology -**

The various configuration options are:
- Number of worker processes
- Number of executors (threads)
- Number of tasks


Refer for more: [Understanding the Parallelism of a Storm Topology](https://storm.apache.org/releases/2.2.0/Understanding-the-parallelism-of-a-Storm-topology.html)


 A topology is a graph of stream transformations where each node is a spout or bolt. Edges in the graph indicate which bolts are subscribing to which streams. When a spout or bolt emits a tuple to a stream, it sends the tuple to every bolt that subscribed to that stream. Topologies are built in Storm using the `TopologyBuilder` class.

![Storm Topology](https://storm.apache.org/releases/2.2.0/images/topology.png)

Each node in a Storm topology executes in parallel. In your topology, you can specify how much parallelism you want for each node, and then Storm will spawn that number of threads across the cluster to do the execution.

A topology runs forever, or until you kill it. Storm will automatically reassign any failed tasks. Additionally, Storm guarantees that there will be no data loss, even if machines go down and messages are dropped.

A simple topology built using TopologyBuilder:

    TopologyBuilder builder = new TopologyBuilder();        
    builder.setSpout("words", new TestWordSpout(), 10);        
    builder.setBolt("exclaim1", new ExclamationBolt(), 3)
            .shuffleGrouping("words");
    builder.setBolt("exclaim2", new ExclamationBolt(), 2)
            .shuffleGrouping("exclaim1");

### Stream groupings

A stream grouping tells a topology how to send tuples between two components.
- Shuffle Groupings - used to distribute data among the Bolt tasks. This method randomly shuffles each data element,
  called a Tuple, among the Bolt tasks such that each task gets roughly the same amount of data.
- Field Groupings - uses one or more of the named elements of a tuple, which are defined by the input vertex, to
  determine the task that will receive a particular data element.
- All Grouping - The allGrouping method ensures that all tuples in an event stream are transmitted to all running tasks
for a particular bolt.
- Global Groupings - ensures that all tuples from a stream go to the bolt with the lowest numbered identifier.
 All bolt tasks receive an identifier number, but this ensures only one of them will be used.
 This should also be used with care because it effectively disables Storm's parallelism.
- Direct Groupings - special form of grouping that allows the output Bolt or Spout to decide which Bolt task receives
   a particular Tuple.
- Custom Groupings - Custom groupings can be implemented by writing a class that implements `CustomStreamGrouping` interface.


### Implementing Bolts

A bolt maybe impletemented by implementing IBasicBolt or IRichBolt interfaces. But the recomemnded approach is to 
extend the BaseBasicBolt or BaseRichBolt class.

- Rich Bolts - 
  Built by extending RichBaseBolt abstract class and defining the three required methods.
- Basic Bolt - 
  It does not have a prepare step and assumes that all tuples will be acknowledged using ack.



