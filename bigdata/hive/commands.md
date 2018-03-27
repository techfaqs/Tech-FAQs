# Hive LOAD and INSERT statements 

## Loading files into tables

Hive does not do any transformation while loading data into tables. Load operations are currently pure copy/move operations that move datafiles into locations corresponding to Hive tables.

    LOAD DATA [LOCAL] INPATH 'filepath' [OVERWRITE] INTO TABLE tablename [PARTITION (partcol1=val1, partcol2=val2 ...)]

## Inserting data into Hive Tables from queries

    INSERT INTO TABLE table_name SELECT columnlist FROM secondtable;

    INSERT INTO TABLE table_name (column_name  data_type)
     PARTITION (columns_name  data_type) VALUES( value1, value2…);
           
    INSERT OVERWRITE TABLE table_name (column_name  data_type) 
     PARTITION (columns_name  data_type) VALUES( value1, value2…)
     LIMIT 3;
     
`INSERT OVERWRITE` will overwrite any existing data in the table or partition
unless `IF NOT EXISTS` is provided for a partition (as of Hive `0.9.0`).
As of Hive `2.3.0`, if the table has `TBLPROPERTIES ("auto.purge"="true")` the previous data of the table is not moved to Trash when `INSERT OVERWRITE` query is run against the table. This functionality is applicable only for managed tables and is turned off when `"auto.purge"` property is unset or set to `false`.

