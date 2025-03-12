# PostgreSQL Update

The `UPDATE` statement is used to modify the value(s) in existing records in a table.

Set the color of the Volvo to 'red':

```bash
UPDATE cars
SET color = 'red'
WHERE brand = 'Volvo';
```

**Note:** Be careful with the `WHERE` clause, in the example above ALL rows where brand = 'Volvo' gets updated.

## Warning! Remember WHERE

Be careful when updating records. If you omit the `WHERE` clause, ALL records will be updated!

## Update Multiple Columns

To update more than one column, separate the name/value pairs with a comma `,`:

Update color and year for the Toyota:

```bash
UPDATE cars
SET color = 'white', year = 1970
WHERE brand = 'Toyota';
```