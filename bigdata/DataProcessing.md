# Data Processing

## Distributed stream data processing

 Immense amounts of data have to be processed fast from a rapidly growing set of disparate data sources.
This pushes the limits of traditional data processing infrastructures. These stream-based applications include trading,
 social networks, Internet of things, system monitoring, and many other examples.

Core features of stream processing frameworks are -

- Coordination
- Partitions and Merges
- Transactions


### Tools

- Apache Storm
- Apache Flink


## Stream Processing

Types of Stream Processing:
- Native Streaming - every incoming record is processed as soon as it arrives, without any wait.
- Micro-batching - incoming records are batched together and then processed in a single mini batch with delay of few seconds.

### Stream Joins

- Stream-Stream Joins (windowing based)
  - One window join
  - Two window based join
- Stream-Table Joins (also called stream enrichment)

### Analysis of stream data

Aggregation on streaming data is generally performed with windowing as streams are never ending!

**Types of queries -**

- Ad-hoc queries (one-time queries)
   Eg: Most purchased item in the 2nd week of April this year? (in retail domain)

- Continueous queries (registers once and runs till they are killed)
   Eg: What is the minimum sales value seen in sales order stream in last hour? (to be computed every hour)


Constraints with Streaming queries -
- Most data based algorithms/models have a one pass approach (data is processon only once, generally to train the model)
- Statistical changes - Stats computed initially keep changing as new data flows in.
- Resource Constraints - No control over frequency of arrival of data(records maybe lost if they are more than window size)
- Domain Constraints - Law or Business constraints (Eg: GDPR, CCPA, etc)


### Types of windows for aggregations

1. Sliding-length window
2. Batch-length window
3. Sliding-time window
4. Batch-time window

----

Counts, Sum, Average, etc are the usual aggreagtion operations performed. Streams also have other aggregates and stats.

- `followed by`/`happens after` relationship reprsented as `->`

        Example: 
           A -> B means "B happened after A" or "A is followed by B"
           A->B?->C means A optionally followed by B and then C
           A->B*->C means A followed by any number of Bs and then C

- Simple Time Series Models
    - Simple Moving Average - Average of values over a sliding window of values
    - Weighted Moving Average - moving average with different weights attached to each value in the window
    - Exponential Moving Average - moving average but places more weight on recent observations than older observations

          Exponential Moving Average(EMA) = a * X + ( 1 – a) * EMA
                                              where a = (2 / (k + 1))

- Linear Models
- Neural nets






