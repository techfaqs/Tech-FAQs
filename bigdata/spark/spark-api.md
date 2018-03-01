# Spark APIs

![History of Spark](https://i.stack.imgur.com/3rF6p.png)

The **RDD** (Resilient Distributed Dataset) API has been in Spark since the 1.0 release. 
From a developer’s perspective, an RDD is simply a set of Java or Scala objects representing data.
The RDD API provides many transformation methods, such as `map()`, `filter()`, and `reduce()` for performing computations on the data.
Each of these methods results in a new RDD representing the transformed data.
However, these methods are just defining the operations to be performed
and the transformations are not performed until an action method is called.
Examples of action methods are `collect()` and `saveAsObjectFile()`.

The main advantage of RDDs is that they are simple and well understood because they deal with concrete classes,
providing a familiar object-oriented programming style with compile-time type-safety.
The main disadvantage to RDDs is that, whenever Spark needs to distribute the data within the cluster, or write the data to disk,
it does so using Java serialization by default (although it is possible to use Kryo as a faster alternative in most cases).
The overhead of serializing individual Java and Scala objects is expensive and requires sending both data and structure between nodes
(each serialized object contains the class structure as well as the values).
There is also the overhead of garbage collection that results from creating and destroying individual objects.

**DataFrame API** was introduced in Spark 1.3 as part of the Project Tungsten initiative,
which seeks to improve the performance and scalability of Spark.
The DataFrame API introduces the concept of a schema to describe the data, allowing Spark to manage the schema
and only pass data between nodes, in a much more efficient way than using Java serialization. 
Another advantage is when performing computations in a single process,
Spark can serialize the data into off-heap storage in a binary format
and then perform many transformations directly on this off-heap memory,
avoiding the garbage-collection costs associated with constructing individual objects for each row in the data set.
And as Spark understands the schema, there is no need to use Java serialization to encode the data.

*The DataFrame API is radically different from the RDD API because it is an API for building a relational query plan that Spark’s Catalyst optimizer can then execute.*

Disadvantages of dataframes, as the code is referring to data attributes by name it is not possible for the compiler to catch any errors.
If attribute names are incorrect then the error will only be detected at runtime, when the query plan is created.
Also DFs are a little Scala-centric, for example when creating a DataFrame from an existing RDD of Java objects,
Spark’s Catalyst optimizer cannot infer the schema and assumes that any objects in the DataFrame implement the `scala.Product` interface.
Scala case classes work out the box because they implement this interface

The **Dataset API**, released as an API preview in Spark 1.6, aims to provide the best of both worlds;
the familiar object-oriented programming style and compile-time type-safety of the RDD API
but with the performance benefits of the Catalyst query optimizer.

When it comes to serializing data, the Dataset API has the concept of encoders which translate between JVM representations (objects) and Spark’s internal binary format.
Spark has built-in encoders which are generate byte code to interact with off-heap data and provide on-demand access to individual attributes without having to de-serialize an entire object.
Datasets also use the same efficient off-heap storage mechanism as the DataFrame API.


#### Reference

[RDD, DF and DS comparision](http://www.agildata.com/apache-spark-rdd-vs-dataframe-vs-dataset/)
