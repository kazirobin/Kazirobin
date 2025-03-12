# PostgreSQL Select Data

To retrieve data from a database, we use the `SELECT` statement.

### Specify Columns

By specifying the column names, we can choose which columns to select:

```bash
SELECT customer_name, country FROM customers;
```

### Return ALL Columns

Specify a `*` instead of the column names to select *all* columns:

```bash
SELECT * FROM customers;
```