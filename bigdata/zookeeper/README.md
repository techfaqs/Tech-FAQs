# ZooKeeper

The ZooKeeper project is a distributed configuration and coordination tool used to coordinate many of the other
 distributed systems.

The ZooKeeper project was developed at Yahoo! It was developed to coordinate the services in the Hadoop environment
which was build by them. It was later open sourced and contributed to the Apache Foundation.
It is used by many systems like Storm, Kafka, Samza, etc.

ZooKeeper(ZK) has a concept of recipes which are to be updated by the application author in order to use ZK in the
 application.

ZooKeeper was designed to store coordination data: status information, configuration, location information, etc.,
 so the data stored at each node is usually small, in the byte to kilobyte range.
 We use the term znode to make it clear that we are talking about ZooKeeper data nodes.

ZK's core data structure is the **`znode`**. These nodes hold data and can be hierarchically be arranged into a tree structure.
Zk isn't intended to be bulk storage hence znodes hold only about 1MB of data and doesn't allow partial reads/write/append.
These are essentially files/directories.

#### ZK Guarantees -

- Sequential Consistency - Updates from a client will be applied in the order that they were sent.
- Atomicity - Updates either succeed or fail. No partial results.
- Single System Image - A client will see the same view of the service regardless of the server that it connects to.
- Reliability - Once an update has been applied, it will persist from that time forward until a client overwrites the update.
- Timeliness - The clients view of the system is guaranteed to be up-to-date within a certain time bound.


#### znode API had 6 operations:

- create - to create a znode at path given as input with the data (optional), if it doesn't exist.
- delete - to remove a znode from the hierarchy
- exists - to check if a znode exists in the path(given as input), without reading data.
- setdata - Similar to `create`, but overwrite the znode if it already exists.
- getData - to retrieve data block from znode.
- getChildern - to retrieve a list of all childern of the znode at the specified path.

> A `znode` maybe persistent or ephemeral.
>
> - Persistent node - these are only deleted when when delete operation is called.
> - Ephermeral node - these are deleted either when delete is called or the client session that created it ends
>   (or is terminated - might also be dure to a heartbeat timeout).
>
> A znode may also be a Sequential node which is a znode created by appending a monotonically increasing number,
>  hence ensuring unique node names and providing a sorting mechanism when requsting for childern of a parent node.
> This is use for leader election.

znodes have versions! The version numbers are given as the nodes are created and updated everytime the data associated
  with the node changes. It maybe optionally passed to delete/setData operations which allows clients to ensure that
 they do not accidentally overwrite changes to a node.

The primary use case for ZooKeeper involves waiting for events, which are changes to data associated with a znode or
 with the children of the znodes. ZK uses notifications to inform clients of changes, called **watches**.
Clients may register a watch with ZK to be informed of changes on a perticuler znode path, this is a one-time
 operation so when a notification is fired the client will have to re-register to recieve the next notification.
This may cause missed notifications in cases where client takes time to set a watch while the state of the znode
 changes, hence ZK allows setting a watch to read data from the znode and coalesce notifications.

ZK uses Zab concenses algorithm, that operates on the order of changes to state as opposed to updating entire state
 when changes are made(like in Paxos algorithm - famous consenses based alogorithm)

> [Paxos](https://www.cs.rutgers.edu/~pxk/417/notes/paxos.html) is a family of protocols for solving consensus in a network
 of unreliable processors (that is, processors that may fail). Consensus is the process of agreeing on one result among
 a group of participants. This problem becomes difficult when the participants or their communication medium may
 experience failures.

### ZK Components

![ZooKeeper Components](https://zookeeper.apache.org/doc/r3.2.2/images/zkcomponents.jpg)

