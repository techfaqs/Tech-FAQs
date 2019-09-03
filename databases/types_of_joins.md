# Types of Joins

Below is a list of various types of joins in RDBMS -

1. INNER JOIN (selects records that have matching values in both tables)

       SELECT * FROM TABLE1 T1 INNER JOIN TABLE T2 ON T1.id = T2.id;
    
2. LEFT OUTER JOIN (all records from the left table, and the matched records from the right table)

       SELECT * FROM TABLE1 T1 LEFT OUTER JOIN TABLE T2 ON T1.id = T2.id;
    
3. RIGHT OUTER JOIN (all records from the right table, and the matched records from the left table)

       SELECT * FROM TABLE1 T1 LEFT OUTER JOIN TABLE T2 ON T1.id = T2.id;
    
4. FULL OUTER JOIN (all records when there is a match in either left or right table)
    
       SELECT * FROM TABLE1 T1 FULL OUTER JOIN TABLE T2 ON T1.id = T2.id;

![inner](https://www.w3schools.com/sql/img_innerjoin.gif)
![left_outer](https://www.w3schools.com/sql/img_leftjoin.gif)
![right_outer](https://www.w3schools.com/sql/img_rightjoin.gif)
![full_outer](https://www.w3schools.com/sql/img_fulljoin.gif)

5. CROSS JOIN (produces a cartesian product between the two tables)

       SELECT * FROM TABLE1 T1 CROSS JOIN TABLE T2;

**Note:**
  -  Number of rows returned by FULL OUTER JOIN equal to `(No. of rows in LEFT OUTER JOIN) + (No. of Rows in RIGHT OUTER JOIN) - (No. of Rows in INNER JOIN)`
  -  Number of rows returned by CROSS JOIN equals to `(No. of rows in LEFT table) x (No. of rows in RIGHT table)`


Images used are from: [w3schools](https://www.w3schools.com/sql/sql_join.asp)
