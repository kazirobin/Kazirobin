# PostgreSQL Select Data

To retrieve data from a database, we use the `SELECT` statement.

## Specify Columns

By specifying the column names, we can choose which columns to select:

```bash
SELECT brand, year FROM cars;
```

## Return ALL Columns

Specify a `*` instead of the column names to select *all* columns:

```bash
SELECT * FROM cars;
```