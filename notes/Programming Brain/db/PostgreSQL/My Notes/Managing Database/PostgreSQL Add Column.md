# PostgreSQL Add Column

To add a column to an existing table, we have to use the `ALTER TABLE` statement. The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table. The `ALTER TABLE` statement is also used to add and drop various constraints on an existing table.

## Add Column

We want to add a column named `color` to our `cars` table.

When adding columns we must also specify the data type of the column. Our `color` column will be a string, and we specify string types with the `VARCHAR` keyword. we also want to restrict the number of characters to 255:

```bash
ALTER TABLE cars
ADD color VARCHAR(255);
```