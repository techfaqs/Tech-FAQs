# Flume

Distributed Log Collection

Flume is a distributed, reliable, and available service for efficiently collecting, aggregating, and moving large
 amounts of log data. It has a simple and flexible architecture based on streaming data flows. It is robust and
 fault tolerant with tunable reliability mechanisms and many failover and recovery mechanisms. It uses a simple
 extensible data model that allows for online analytic application.

Flume can be used to transport massive quantities of event data including but not limited to network traffic data,
 social-media-generated data, email messages and pretty much any data source possible.


![Flume block diagram](https://flume.apache.org/_images/DevGuide_image00.png)


- **Sources** are components that either retrieve or receive data from an outside source and transfer it into one or more channels.
- **Channel** defines the the persistence and transaction semantics. Its a passive store that keeps the event until it’s consumed by a Flume sink.
- **Sinks** removes the event from the channel and puts it into an external repository like HDFS (via Flume HDFS sink) or
   forwards it to the Flume source of the next Flume agent (next hop) in the flow.

Flume allows a user to build multi-hop flows where events travel through multiple agents before reaching the final destination.
 It also allows fan-in and fan-out flows, contextual routing and backup routes (fail-over) for failed hops.

Flume provide end-to-end **reliability** of the flow, as events are removed from a channel only after they are stored in
 the channel of next agent or in the terminal repository.

Flume supports a durable file channel which is backed by the local file system, this helps in **recoverability**. There’s
 also a memory channel which simply stores the events in an in-memory queue, which is faster but any events still left
 in the memory channel when an agent process dies can’t be recovered.

Data distribution between source and the channels is as per the channel selector. Various channel selectors are:
- Replicating Selector - takes all inputs and sends them to all channels for further processing. Its the default.
  It can also be set to ignore write failures to certain channels using,
       <agent>.source.<source>.selector.optional = <channel>
- Multiplexing Selector - it distributs data across different channels depending on the Event's header metadata.
  By default, the channel is determined from the flume.selector.header header in the metadata, but it can be changed
  with the `selector.header` property. Eg: `agent_1.source.source-1.selector.header= timezone`

  The target channel(s) is specified with the `selector.mapping` property. The values must be explicitly mapped for each possible value with
 a default channel specified with the `selector.default` property. Explicitly specify the mapping of a header to a channel significantly
 reduces the utility of the multiplexing selector. A better choice would be a load-balancing sink processor.

- Custom Selectors - these can be defined and used by specifying the fully qualified class name as the `selector.type`.

Example:

      agent_1.source.source-1.selector.type = wiley.streaming.flume.RandomSelector


## Flume Sources

One of the chief draws for Flume is its ability to integrate with a variety of systems. To support this,
Flume ships with a number of built-in source components.

- Avro Source
- Thrift Source - to integrate with existing Thrift/Scribe pipelines.
- Netcat Source - reads in newline-delimited text lines with, by default, a maximum length of 512 bytes.
  To increase this limit `max-line-length` maybe updated. Acknowledgement for every event is set to true by default,
   but this can be changed by updating `ack-every-event` property.
- Syslog Source - Syslog is a standard for systems logging that was originally developed as part of the Sendmail
package in the 1980s. The maximum size of the events is controlled with the eventSize property, which defaults to 2,500
bytes, this can be changed by updating `eventSize` property.

- HTTP Source - allows Flume to accept events from services that can make HTTP requests.For many potential event sources,
 this offers the ability to also add rich metadata headers to the event without having to implement a custom source.
 Events are transmitted to the HTTP source using the POST command and return either a `200` or a `503` response code.
 The 503 response code is used when a channel is full or otherwise disabled. An application, upon receiving this event,
 should retry sending the event through some other mechanism.

  After the event arrives at the HTTP source it must be converted into Flume events. This is done using a pluggable
 *Handler class*, with a `JSONHandler` and a `BlobHandler` class provided by Flume.
 The handler, which is set to the JSONHandler by default, is controlled by the handler property. This property takes a
  fully qualified class name of a class that implements the `HTTPSourceHandler` interface:
       agent_1.source.source-1.handler=org.apache.flume.source.http.JSONHandler

> Events are buffered in memory, so very large elements could fill the Java heap allocated to the Flume
process. This causes Flume to crash and, depending on the channel, could cause a loss of data.
Therefore, it is important to restrict the size of objects sent to a BlobHandler.

- Java Message Service (JMS) Source - allows Flume to integrate with Java-based queuing systems.
- Exec Source - allows any command to be used as input to stream.

Example:

    agent_1.source.source-1.type= exec
    agent_1.source.source-1.command= tail –F /var/log/logfile.log
    
A shell can be specified with the `shell` property. A command can be restarted once it exists using `restart` property.
`restartThrottle` property may be used to define how quickly the command should restart.
Exec by default reads from std input but it can be configured to read from std Error using `logStdErr` property.

To improve performance, the Exec source reads a batch of lines before sending them on to their
assigned channel(s). By deafult its 20 lines, `batchSize` property may be used to change it.

- Custom Source - a Pollable source(executed by Flume in their own thread and queried repeatedly to move data onto its associated channels)
   and an Event-Driven source(maintains its own thread and places events on its channel asynchronously) may be created.


## Flume Sinks

- HDFS Sink - writes events into the Hadoop Distributed File System, it can create text and sequence files.
   It supports compression in both file types. The files can be rolled (close current file and create a new one) periodically
  based on the elapsed time or size of data or number of events. It also buckets/partitions data by attributes like
  timestamp or machine where the event originated.
- Hive Sink
- Avro Sink
- Thrift Sink
- IRC Sink
- File Roll Sink
- HBase Sink
- HTTP Sink
- Custom Sink


## Flume Channels

Channels are the repositories where the events are staged on a agent. Source adds the events and Sink removes it.

- Memory Channel - The events are stored in an in-memory queue with configurable max size. It’s ideal for flows that need
  higher throughput and are prepared to lose the staged data in the event of a agent failures.
- JDBC Channel - The events are stored in a persistent storage that’s backed by a database. The JDBC channel currently supports
 embedded Derby. This is a durable channel that’s ideal for flows where recoverability is important.
- Kafka Channel - The events are stored in a Kafka cluster
- File Channel
- Spillable Memory Channel(experimental) - The events are stored in an in-memory queue and on disk. The in-memory queue
  serves as the primary store and the disk as overflow. The disk store is managed using an embedded File channel. 
  When the in-memory queue is full, additional incoming events are stored in the file channel.

- Custom Channel


## Flume Interceptors

Flume has the capability to modify/drop events in-flight. This is done with the help of interceptors.
Interceptors are classes that implement `org.apache.flume.interceptor.Interceptor` interface.
An interceptor can modify or even drop events based on any criteria chosen by the developer of the interceptor.

- Timestamp Interceptor - adds the current timestamp as a metadata header on the event with the key `timestamp`.
  `preserveExisting` property can be used to control whether to overwrite if it exists.
- Host Interceptor - attaches either the hostname of the Flume agent or the IP address to the header metadata. 
  The default header is called host, but it can be changed using the hostHeader property.
- Static Interceptor - used to add a static header to all events.
- UUID Interceptor - adds a globally unique identifier to each event.
- Regular Expression Filter Interceptor


