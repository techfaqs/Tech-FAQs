# Hive insert statements

```INSERT INTO TABLE table_name SELECT columnlist FROM secondtable;```
```
   INSERT INTO TABLE table_name (column_name  data_type)
      PARTITION (columns_name  data_type) VALUES( value1, value2…);
```
   - The **INSERT INTO** syntax appends data to a table. The existing data files are left as-is, and the inserted data is put 
     into one or more new data files.
```
   INSERT OVERWRITE TABLE table_name (column_name  data_type)
     PARTITION (columns_name  data_type) VALUES( value1, value2…)
      LIMIT 3;
```
   - The **INSERT OVERWRITE** syntax replaces the data in a table. Currently, the overwritten data files are deleted immediately; 
     they do not go through the HDFS trash mechanism.

```INSERT INTO TABLE table_name SELECT * FROM some_other_table;```
    
```create table t1 ( i int ) partitioned by (x int , y string);```

``` INSERT INTO t1 PARTITION ( x=10, y=’a’ ) SELECT c1 FROM some_other table; ```

   - All inserted rows will have the same x and y values. This technique of specifiying all the partition key values is known as static       partitioning.

   - If you want to use Static partition in Hive you should set property 
      ``` set hive.mapred.mode = strict ``` 
          This property set by default in hive-site.xml.

``` INSERT INTO t1 PARTITION ( x, y=’b’ ) SELECT c1, c2 from some_other_table; ```

   - All inserted rows will have the same y value.

   - Any partitioning columns whose value is not specified are filled in from the columns specified last in the SELECT list.

   - This technique of omitting some partition key values is known as Dynamic Partitioning.

  - To do dynamic partition, we have to set property  
     ``` set hive.exec.dynamic.partition.mode = True ```

