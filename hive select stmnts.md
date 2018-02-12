## Hive select statements:

- Retrieving Information (General)

  ``` SELECT from_columns FROM table WHERE conditions;```
  
- Retrieving All Values

   ```SELECT * FROM table;```
 
- Retrieving Some Values

  ```SELECT * FROM table WHERE rec_name = "value";```

- Retrieving With Multiple Criteria

  ```SELECT * FROM TABLE WHERE rec1= "value1" AND rec2 ="value2";```

- Retrieving Specific Columns

  ```SELECT column_name FROM table;```

- Retrieving Unique Output

  ```SELECT DISTINCT column_name FROM table;```

- Counting Rows

  ```SELECT COUNT(*) FROM table;```

- Grouping With Counting

  ```SELECT owner, COUNT(*) FROM table GROUP BY owner;```

- Maximum Value

  ```SELECT MAX(col_name) AS label FROM table;```

#### Order by:
Order by clause use columns on Hive tables for grouping particular column values mentioned with Order by. For whatever the column name we are defining the order by clause the query will selects and display results by ascending or descending order the particular column values.

**Example:**
  
  ```SELECT * FROM employees ORDER BY department;```
#### Group by query:
Group by clause use columns on Hive tables for grouping particular column values mentioned with the group by. For whatever the column name we are defining a "groupby" clause the query will selects and display results by grouping the particular column values.

**Example:**
  
  ```SELECT department, count(*) from employees GROUP BY department;```
#### Sort by:
Sort by clause performs on column names of Hive tables to sort the output. We can mention DESC for sorting the order in descending order and mention ASC for Ascending order of the sort.
In this sort by it will sort the rows before feeding to the reducer. Always sort by depends on column types.

**Example:**
  
  ```SELECT * FROM employees SORT BY id DESC;```
#### Cluster By:
- Cluster By used as an alternative for both Distribute BY and Sort BY clauses in Hive-QL.
- Cluster BY clause used on tables present in Hive. Hive uses the columns in Cluster by to distribute the rows among reducers. Cluster BY columns will go to the multiple reducers.It ensures sorting orders of values present in multiple reducers
- For example, Cluster By clause mentioned on the Id column name of the table employees table. The output when executing this query will give results to multiple reducers at the back end. But as front end it is an alternative clause for both Sort By and Distribute By.
- This is actually back end process when we perform a query with sort by, group by, and cluster by in terms of Map reduce framework. So if we want to store results into multiple reducers, we go with Cluster By.

**Example:**

  ```Select id, name from employees cluster by id;```
#### Distribute By:
Distribute BY clause used on tables present in Hive. Hive uses the columns in Distribute by to distribute the rows among reducers. All Distribute BY columns will go to the same reducer.
- It ensures each of N reducers gets non-overlapping ranges of column
- It doesn't sort the output of each reducer

**Example:**

  ```SELECT Id, Name FROM employees DISTRIBUTE BY Id;```

**NOTE:**
-  **ORDER BY x:** guarantees global ordering, but does this by pushing all data through just one reducer. This is basically unacceptable for large datasets. You end up one sorted file as output.

- **SORT BY x:** orders data at each of N reducers, but each reducer can receive overlapping ranges of data. You end up with N or more sorted files with overlapping ranges.

- **DISTRIBUTE BY x:** ensures each of N reducers gets non-overlapping ranges of x, but doesn't sort the output of each reducer. You end up with N or unsorted files with non-overlapping ranges.

- **CLUSTER BY x:** ensures each of N reducers gets non-overlapping ranges, then sorts by those ranges at the reducers. This gives you global ordering, and is the same as doing (DISTRIBUTE BY x and SORT BY x). You end up with N or more sorted files with non-overlapping ranges.



