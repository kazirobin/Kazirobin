# PostgreSQL ORDER BY

The `ORDER BY` keyword is used to sort the result in ascending or descending order. The `ORDER BY` keyword sorts the records in ascending order by default. To sort the records in descending order, use the `DESC` keyword.

Sort the table by price:

```bash
SELECT * FROM products ORDER BY price;
```

### DESC

The `ORDER BY` keyword sorts the records in ascending order by default. To sort the records in descending order, use the `DESC` keyword.

Sort the table by price, in descending order:

```bash
SELECT * FROM products ORDER BY price DESC;
```

### Sort Alphabetically

For string values the `ORDER BY` keyword will order alphabetically:

Sort the table by product name:

```bash
SELECT * FROM products ORDER BY product_name;
```

### Alphabetically DESC

To sort the table reverse alphabetically, use the `DESC` keyword:

Sort the table by product name, in descending order:

```bash
SELECT * FROM products ORDER BY product_name DESC;
```