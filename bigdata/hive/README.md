# Hive

Hive is a data warehousing infrastructure based on Apache Hadoop.
Hadoop provides massive scale out and fault tolerance capabilities for data
 storage and processing on commodity hardware.
 
Hive is not designed for online transaction processing.
It is best used for traditional data warehousing tasks.


### Data Units

In the order of granularity - Hive data is organized into:
Databases: Namespaces function to avoid naming conflicts for tables, views,
partitions, columns, and so on.  Databases can also be used to enforce security
for a user or group of users.
Tables: Homogeneous units of data which have the same schema. An example of
a table could be page_views table, where each row could comprise of the
following columns (schema):

* `timestamp` — which is of `INT` type that corresponds to a UNIX timestamp
   of when the page was viewed.
* `userid` —which is of `BIGINT` type that identifies the user who viewed
   the page.
* `page_url`—which is of `STRING` type that captures the location of the page.
* `referer_url`—which is of STRING that captures the location of the page
   from where the user arrived at the current page.
* `IP`—which is of `STRING` type that captures the IP address from where
   the page request was made.
* `Partitions`: Each Table can have one or more partition Keys which
   determines how the data is stored. Partitions—apart from being storage
   units—also allow the user to efficiently identify the rows that satisfy
   a specified criteria; for example, a date_partition of type STRING and
   country_partition of type STRING.
   Each unique value of the partition keys defines a partition of the Table.
   
   __For example__ , all "US" data from "2009-12-23" is a partition of the
   page_views table. Therefore, if you run analysis on only the "US" data
   for 2009-12-23, you can run that query only on the relevant partition of
   the table, thereby speeding up the analysis significantly.
   __Note__ however, that just because a partition is named 2009-12-23 does not mean
   that it contains all or only data from that date; partitions are named after
   dates for convenience; it is the user's job to guarantee the relationship
   between partition name and data content! Partition columns are virtual columns,
   they are not part of the data itself but are derived on load.
* `Buckets` (or `Clusters`): Data in each partition may in turn be divided into
   Buckets based on the value of a hash function of some column of the Table.
   __For example__ the page_views table may be bucketed by userid, which is one
   of the columns, other than the partitions columns, of the page_view table.
   These can be used to efficiently sample the data.

__Note__ that it is not necessary for tables to be partitioned or bucketed,
but these abstractions allow the system to prune large quantities of data during
query processing, resulting in faster query execution.

Reference: [Apache Hive Tutorial](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-WhatIsHive)
