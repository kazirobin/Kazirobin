# PostgreSQL Left Join

The `LEFT JOIN` keyword selects ALL records from the "left" table, and the matching records from the "right" table. The result is 0 records from the right side if there is no match.

Let's look at an example using our dummy `testproducts` table:

```bash
 testproduct_id |      product_name      | category_id
----------------+------------------------+-------------
              1 | Johns Fruit Cake       |           3
              2 | Marys Healthy Mix      |           9
              3 | Peters Scary Stuff     |          10
              4 | Jims Secret Recipe     |          11
              5 | Elisabeths Best Apples |          12
              6 | Janes Favorite Cheese  |           4
              7 | Billys Home Made Pizza |          13
              8 | Ellas Special Salmon   |           8
              9 | Roberts Rich Spaghetti |           5
            10 | Mias Popular Ice        |          14
(10 rows)
```

We will try to join the `testproducts` table with the `categories` table:

```bash
 category_id | category_name  |                       description
-------------+----------------+------------------------------------------------------------
           1 | Beverages      | Soft drinks, coffees, teas, beers, and ales
           2 | Condiments     | Sweet and savory sauces, relishes, spreads, and seasonings
           3 | Confections    | Desserts, candies, and sweet breads
           4 | Dairy Products | Cheeses
           5 | Grains/Cereals | Breads, crackers, pasta, and cereal
           6 | Meat/Poultry   | Prepared meats
           7 | Produce        | Dried fruit and bean curd
           8 | Seafood        | Seaweed and fish
(8 rows)
```

**Note:** Many of the products in `testproducts` have a `category_id` that does not match any of the categories in the `categories` table.

By using `LEFT JOIN` we will get all records from `testpoducts`, even the ones with no match in the `categories` table:

Join `testproducts` to `categories` using the `category_id` column:

```bash
SELECT testproduct_id, product_name, category_name
FROM testproducts
LEFT JOIN categories ON testproducts.category_id = categories.category_id;
```

All records from `testproducts`, and only the matched records from `categories`:

```bash
 testproduct_id |      product_name      | category_name
----------------+------------------------+----------------
              1 | Johns Fruit Cake       | Confections
              2 | Marys Healthy Mix      |
              3 | Peters Scary Stuff     |
              4 | Jims Secret Recipe     |
              5 | Elisabeths Best Apples |
              6 | Janes Favorite Cheese  | Dairy Products
              7 | Billys Home Made Pizza |
              8 | Ellas Special Salmon   | Seafood
              9 | Roberts Rich Spaghetti | Grains/Cereals
             10 | Mias Popular Ice       |
(10 rows)
```

**Note:** `LEFT JOIN` and `LEFT OUTER JOIN` will give the same result. `OUTER` is the default join type for `LEFT JOIN`, so when you write `LEFT JOIN` the parser actually writes `LEFT OUTER JOIN`.