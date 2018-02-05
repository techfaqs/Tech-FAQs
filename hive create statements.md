## Hive Create table commands
### Internal tables

- Internal Table is tightly coupled in nature.In this type of table, first we have to create table and load the data.
- We can call this one as data on schema.
- By dropping this table, both data and schema will be removed.
- The stored location of this table will be at /user/hive/warehouse.

**When to Choose Internal Table:**
- If the processing data available in local file system
- If we want Hive to manage the complete lifecycle of data including the deletion

**Sample code Snippet for Internal Table:**
```
CREATE TABLE weather (wban INT, date STRING, precip INT) 
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ‘,’ ;
```

### External tables
- External Table is loosely coupled in nature. Data will be available in HDFS.The table is going to create on HDFS data.
- In other way, we can say like its creating schema on data.
- At the time of dropping the table it drops only schema, the data will be still available in HDFS as before.
- External tables provide an option to create multiple schemas for the data stored in HDFS instead of deleting the data every time whenever schema updates

**When to Choose External Table:**
- If processing data available in HDFS
- Useful when the files are being used outside of Hive

**Sample code Snippet for External Table:**
```
CREATE EXTERNAL TABLE weather (wban INT, date STRING, precip INT) 
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ‘,’ 
LOCATION ‘ /hive/data/weather ‘ ;
```
#### Difference between Internal Vs External tables
|Feature|Internal|External|
|-|-|-|
|Schema|Data on Schema|Schema on Data|
|Storage Location|/usr/hive/warehouse|HDFS location|
|Data Availability|Within local file system|Within HDFS|

#### Create table with IF NOT EXISTS: 
If you add the option **IF NOT EXISTS**, Hive ignores the statement in case the table already exists.
Example:
```
CREATE TABLE IF NOT EXISTS employee ( eid int, name String, salary String)
COMMENT ‘Employee details’
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ‘\t’
LINES TERMINATED BY ‘\n’
STORED AS TEXTFILE;
```
### Create table with (PARTITIONED BY/CLUSTERD BY/TBLPROPERTIES clause):
#### Partition by clause:
Table partitioning means dividing table data into some parts based on the values of particular columns like date or country, segregate the input records into different files/directories based on date or country.
Partitioning can be done based on more than column which will impose multi-dimensional structure on directory storage.
We use PARTITION BY clause to divide the data into some parts.

__Advantages__
- Partitioning is used for distributing execution load horizontally.
- As the data is stored as slices/parts, query response time is faster to process the small part of the data instead of looking for a search in the entire data set.
- For example, In a large user table where the table is partitioned by country, then selecting users of country ‘IN’ will just scan one directory ‘country=IN’ instead of all the directories.

**Limitations**
- Having too many partitions in table creates large number of files and directories in HDFS, which is an overhead to NameNode since it must keep all metadata for the file system in memory only.
- Partitions may optimize some queries based on Where clauses, but may be less responsive for other important queries on grouping clauses.

**Example Scenarios**
- Partitioning is used in real-time log files analysis to segregate the records based on time stamp or date value to see the results day wise quickly.
- Another real-time use is that, Customer/user details are partitioned by country/state or department for fast retrieval of subset data pertaining to some category.
- Sales records by-product type, country, year and month is another commonly used scenario.

#### Bucketing (CLUSTERD BY clause)
- Bucketing concept is based on (hashing function on the bucketed column) mod (by total number of buckets). The hash_function depends on the type of the bucketing column.
- Records with the same bucketed column will always be stored in the same bucket.
- We use CLUSTERED BY clause to divide the table into buckets.
- Physically, each bucket is just a file in the table directory, and Bucket numbering is 1-based.
- Bucketing can be done along with Partitioning on Hive tables and even without partitioning.
- Bucketed tables will create almost equally distributed data file parts.

#### TBLPROPERTIES clause:
The **TBLPROPERTIES** clause allows you to tag the table definition with your own metadata key/value pairs.
Example:
```
CREATE TABLE page_view (viewTime INT, userid BIGINT, page_url STRING)
[PARTITIONED BY  (dt STRING, country STRING)
[CLUSTERED BY (userid) SORTED BY (viewTime) INTO 32 BUCKETS]
[TBLPROPERTIES (‘key1’=’value1’, ‘key2’=’value2’, …)]
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '1'
STORED AS SEQUENCEFILE;
```
#### Cloning tables (LIKE clause):
To create an empty table with the same columns, comments, and other attributes as another table, use the following variation. The CREATE TABLE ... LIKE form allows a restricted set of clauses, currently only the LOCATION, COMMENT, and STORED AS clauses.
Example:
```
CREATE TABLE [db.name]table_name
LIKE {[db_name.] table_name}
[COMMENT ‘table_comment’]
[STORED AS file_format]
[LOCATION ‘hdfc_path’]
```
#### CREATE TABLE AS SELECT:
The **CREATE TABLE AS SELECT** syntax is a shorthand notation to create a table based on column definitions from another table, and copy data from the source table to the destination table without issuing any separate INSERT statement.
Example:
```
CREATE TABLE emp2 AS SELECT * FROM emp1;
```






