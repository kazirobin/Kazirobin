# PostgreSQL SELECT DISTINCT

The `SELECT DISTINCT` statement is used to return only distinct (different) values.

Inside a table, a column often contains many duplicate values and sometimes you only want to list the different (distinct) values.

Select only the DISTINCT values from the `country` column in the `customers` table:

```bash
SELECT DISTINCT country FROM customers;
```

### SELECT COUNT(DISTINCT)

We can also use the `DISTINCT` keyword in combination with the `COUNT` statement, which in the example below will return the number of different countries there are in the `customers` table.

Return the number of different countries there are in the `customers` table:

```bash
SELECT COUNT(DISTINCT country) FROM customers;
```