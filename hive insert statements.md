##  Hive insert statements

#### Some insert queries.

1. The below **INSERT INTO** syntax appends data to a table. The existing data files are left as-is, and the inserted data is put 
   into one or more new data files.
  ```
   INSERT INTO TABLE table_name (column_name  data_type)
   PARTITION (columns_name  data_type) VALUES( value1, value2…);
   ```
2.  The below **INSERT OVERWRITE** syntax replaces the data in a table. Currently, the overwritten data files are deleted immediately; 
  they do not go through the HDFS trash mechanism.
  ```
   INSERT OVERWRITE TABLE table_name (column_name  data_type)
   PARTITION (columns_name  data_type) VALUES( value1, value2…)
   LIMIT 3;
   ```
#### Static partition and Dynamic partition in Hive Insert query:

__Static Partition__

   - Insert input data files individually into a partition table is Static Partition.
   - Usually when loading files (big files) into Hive tables static partitions are preferred.
   - Static Partition saves your time in loading data compared to dynamic partition.
   - We can alter the partition in the static partition.
   - You can perform Static partition on Hive Manage table or external table.
   
*Example:*    
*```create table t1 ( i int ) partitioned by (x int , y string);```*

```INSERT INTO t1 PARTITION ( x=10, y=’a’ ) SELECT c1 FROM some_other table;```

   - All inserted rows will have the same x and y values. This technique of specifiying all the partition key values is known as static      partitioning.
   - If you want to use Static partition in Hive you should set property. 
 ``` set hive.mapred.mode = strict ``` 
     This property set by default in hive-site.xml.
   - Static partition is in Strict Mode.

   
__Dynamic Partition__

   - Single insert to partition table is known as a dynamic partition.
   - Dynamic Partition takes more time in loading data compared to static partition.
   - If you want to partition a number of columns but you don’t know how many columns then also dynamic partition is suitable.
   - we can’t perform alter on the Dynamic partition.
   - You can perform dynamic partition on hive external table and managed table.
   - If you want to use the Dynamic partition in the hive then the mode is in non-strict mode.
   
*Example:*    
*```create table t1 ( i int ) partitioned by (x int , y string);```*

```INSERT INTO t1 PARTITION ( x, y=’b’ ) SELECT c1, c2 from some_other_table;```

   - All inserted rows will have the same y value.
   - Any partitioning columns whose value is not specified are filled in from the columns specified last in the SELECT list.
   - This technique of omitting some partition key values is known as Dynamic Partitioning.
   - To do dynamic partition, we have to set property  
     ``` set hive.exec.dynamic.partition.mode = True ```
  - Dynamic partition is in non-strict mode.

