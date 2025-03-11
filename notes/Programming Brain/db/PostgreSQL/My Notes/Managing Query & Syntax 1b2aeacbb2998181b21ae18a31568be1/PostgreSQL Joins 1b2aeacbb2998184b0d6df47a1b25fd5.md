# PostgreSQL Joins

A `JOIN` clause is used to combine rows from two or more tables, based on a related column between them.

Let's look at a selection from the `products` table:

```bash
 product_id |  product_name  | category_id
------------+----------------+-------------
         33 | Geitost        |           4
         34 | Sasquatch Ale  |           1
         35 | Steeleye Stout |           1
         36 | Inlagd Sill    |           8
```

Then, look at a selection from the `categories` table:

```bash
 category_id | category_name
-------------+----------------
           1 | Beverages
           2 | Condiments
           3 | Confections
           4 | Dairy Products
```

Notice that the `category_id` column in the `products` table refers to the `category_id` in the `categories` table. The relationship between the two tables above is the `category_id` column.

Then, we can create the following SQL statement (with a JOIN), that selects records that have matching values in both tables:

Join `products` to `categories` using the `category_id` column:

```bash
SELECT product_id, product_name, category_name
FROM products
INNER JOIN categories ON products.category_id = categories.category_id;
```

If we pull out the same selection from products table above, we get this result:

```bash
 product_id |  product_name  | category_name
------------+----------------+----------------
         33 | Geitost        | Dairy Products
         34 | Sasquatch Ale  | Beverages
         35 | Steeleye Stout | Beverages
         36 | Inlagd Sill    | Seafood
```

## Different Types of Joins

Here are the different types of the Joins in PostgreSQL:

- `INNER JOIN`: Returns records that have matching values in both tables
- `LEFT JOIN`: Returns all records from the left table, and the matched records from the right table
- `RIGHT JOIN`: Returns all records from the right table, and the matched records from the left table
- `FULL JOIN`: Returns all records when there is a match in either left or right table