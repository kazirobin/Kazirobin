# PostgreSQL Drop Column

To remove a column from a table, we have to use the `ALTER TABLE` statement. The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table. The `ALTER TABLE` statement is also used to add and drop various constraints on an existing table.

## Drop Column

We want to remove the column named `color` from the `cars` table. To remove a column, use the `DROP COLUMN` statement:

Remove the `color` column:

```bash
ALTER TABLE cars
DROP COLUMN color;
```