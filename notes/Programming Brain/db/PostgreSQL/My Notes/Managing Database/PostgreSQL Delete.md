# PostgreSQL Delete

The `DELETE` statement is used to delete existing records in a table. To delete the record(s) where the brand is 'Volvo', use this statement:

Delete all records where the brand is 'Volvo':

```bash
DELETE FROM cars
WHERE brand = 'Volvo';
```

**Note:** Be careful when deleting records in a table! Notice the `WHERE` clause in the `DELETE` statement. The `WHERE` clause specifies which record(s) should be deleted.  If you omit the `WHERE` clause, **all records in the table will be deleted**!

## Delete All Records

It is possible to delete all rows in a table without deleting the table. This means that the table structure, attributes, and indexes will be intact. The following SQL statement deletes all rows in the `cars` table, without deleting the table:

Delete all records in the `cars` table:

```bash
DELETE FROM cars;
```

## Truncate Table

Because we omit the `WHERE` clause in the `DELETE` statement above, all records will be deleted from the cars table. The same would have been achieved by using the `TRUNCATE TABLE` statement:

Delete all records in the `cars` table:

```bash
TRUNCATE TABLE cars;
```