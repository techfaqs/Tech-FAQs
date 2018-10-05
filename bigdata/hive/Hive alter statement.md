### Hive alter table commands
#### Table names can be changed and columns can be added or replaced:

- Changing the table name:

  ```ALTER TABLE events RENAME TO 3koobecaf;```

- Adding columns to the table:

  ```ALTER TABLE pokes ADD COLUMNS (new_col INT);```

- Adding columns to the table with comment:

  ```ALTER TABLE invites ADD COLUMNS (new_col2 INT COMMENT 'a comment');```

- Replaces columns in table:

  ```ALTER TABLE invites REPLACE COLUMNS (foo INT, bar STRING, baz INT COMMENT 'baz replaces new_col2');```

**NOTE:**

REPLACE COLUMNS replaces all existing columns and only changes the table's schema, not the data. The table must use a native SerDe. REPLACE COLUMNS can also be used to drop columns from the table's schema:

  ```ALTER TABLE invites REPLACE COLUMNS (foo INT COMMENT 'only keep the first column');```

