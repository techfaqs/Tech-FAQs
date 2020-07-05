# Comparision of the Stream Processing frameworks

### Storm

- Advantages:
    - Very low latency,true streaming, mature and high throughput
    - Excellent for non-complicated streaming use cases
- Disadvantages
    - No implicit support for state management
    - No advanced features like Event time processing, aggregation,windowing,sessions,watermarks,etc
    - Atleast-once guarantee

---

### Spark Streaming

- Advantages:
    - Supports Lambda architecture, comes free with Spark
    - High throughput, good for many use cases where sub-latency is not required
    - Fault tolerance by default due to micro-batch nature
    - Simple to use higher level APIs
    - Big community and aggressive improvements
    - Exactly Once

-  Disadvantages
    - Not true streaming, not suitable for low latency requirements
    - Too many parameters to tune. Hard to get it right. Have written a post on my personal
    experience while tuning Spark Streaming
    - Stateless by nature
    - Lags behind Flink in many advanced features

---

### Flink

- Advantages:
    - Leader of innovation in open source Streaming landscape
    - First True streaming framework with all advanced features like event time
    processing,watermarks,etc
    - Low latency with high throughput, configurable according to requirements
    - Auto-adjusting, not too many parameters to tune
    - Exactly Once
    - Getting widely accepted by big companies at scale like Uber,Alibaba.

- Disadvantages
    - Little late in game, there was lack of adoption initially
    - Community is not as big as Spark but growing at fast pace now
    - No known adoption of the Flink Batch as of now, only popular for streaming.
    
    
---
    
### Samza
    
- Advantages :
    - Very good in maintaining large states of information (good for use case of joining streams)
    using RocksDb and kafka log.
    - Fault Tolerant and High performant using Kafka properties
    - One of the options to consider if already using Yarn and Kafka in the processing pipeline.
    - Good Yarn citizen
    - Low latency , High throughput , mature and tested at scale
    
- Disadvantages :
    - Tightly coupled with Kafka and Yarn. Not easy to use if either of these not in your
    processing pipeline.
    - Atleast-once processing guarantee. Although after Kafka 0.11 release which talks about
    Exactly Once, it might change.
    - Lack of advanced streaming features like Watermarks, Sessions, triggers,etc
    
---
    
## How to Choose the best one for my use-case?

- Depends on the use cases (Granularity, scale, reliability required, accuracy, etc)
- Existing Tech Stack (Compatibility, planning to add this componnet or change existing model?)
- Budget (Investment possible incase of chnage in tool)
- Future Considerations (plan to implement something else or change in requiremnets?)


> It is always advised to start with a *Proof of Concept* to check the fit of the selected tool(s) so as to better evaluate
 it before investing time and money to implement it for your use-case.
 