# PostgreSQL Full Join

The `FULL JOIN` keyword selects ALL records from both tables, even if there is not a match. For rows with a match the values from both tables are available, if there is not a match the empty fields will get the value `NULL`.

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
             10 | Mias Popular Ice       |          14
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

By using `FULL JOIN` we will get all records from both the `categories` table and the `testproducts` table:

Join `testproducts` to `categories` using the `category_id` column:

```bash
SELECT testproduct_id, product_name, category_name
FROM testproducts
FULL JOIN categories ON testproducts.category_id = categories.category_id;
```

All records from both tables are returned.

Rows with no match will get a `NULL` value in fields from the opposite table:

```bash
 testproduct_id |      product_name       | category_name
----------------+-------------------------+----------------
              1 | Johns Fruit Cake        | Confections
              2 | Marys Healthy Mix       |
              3 | Peters Scary Stuff      |
              4 | Jims Secret Recipe      |
              5 | Elisabeths Best Apples  |
              6 | Janes Favorite Cheese   | Dairy Products
              7 | Billys Home Made Pizza  |
              8 | Ellas Special Salmon    | Seafood
              9 | Roberts Rich Spaghetti  | Grains/Cereals
             10 | Mias Popular Ice        |
                |                         | Condiments
                |                         | Meat/Poultry
                |                         | Beverages
                |                         | Produce
(14 rows)
```

**Note:** `FULL JOIN` and `FULL OUTER JOIN` will give the same result. `OUTER` is the default join type for `FULL JOIN`, so when you write `FULL JOIN` the parser actually writes `FULL OUTER JOIN`.