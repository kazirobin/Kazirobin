# PostgreSQL UNION

The `UNION` operator is used to combine the result-set of two or more queries.

The queries in the union must follow these rules:

- They must have the same number of columns
- The columns must have the same data types
- The columns must be in the same order

Combine `products` and `testproducts` using the `UNION` operator:

```bash
SELECT product_id, product_name
FROM products
UNION
SELECT testproduct_id, product_name
FROM testproducts
ORDER BY product_id;
```

## UNION vs UNION ALL

With the `UNION` operator, if some rows in the two queries returns the exact same result, only one row will be listed, because `UNION` selects only distinct values.

Use `UNION ALL` to return duplicate values.

Let's make some changes to the queries, so that we have duplicate values in the result:

### Example - UNION

```bash
SELECT product_id
FROM products
UNION
SELECT testproduct_id
FROM testproducts
ORDER BY product_id;
```

### Example - UNION ALL

```bash
SELECT product_id
FROM products
UNION ALL
SELECT testproduct_id
FROM testproducts
ORDER BY product_id;
```