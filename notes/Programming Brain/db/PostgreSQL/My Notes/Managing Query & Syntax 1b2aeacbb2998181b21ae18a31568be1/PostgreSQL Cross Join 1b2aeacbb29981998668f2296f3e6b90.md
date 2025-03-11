# PostgreSQL Cross Join

The `CROSS JOIN` keyword matches ALL records from the "left" table with EACH record from the "right" table.  That means that all records from the "right" table will be returned for each record in the "left" table. This way of joining can potentially return very large table, and you should not use it if you do not have to.

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

**Note:** The `CROSS JOIN` method will return ALL `categories` for EACH `testproduct`, meaning that it will return 80 rows (10 * 8).

Join `testproducts` to `categories` using the `CROSS JOIN` keyword:

```bash
SELECT testproduct_id, product_name, category_name
FROM testproducts
CROSS JOIN categories;
```

All `categories` for each `testproduct` will be returned:

```bash
 testproduct_id |      product_name      | category_name
----------------+------------------------+----------------
              1 | Johns Fruit Cake       | Beverages
              1 | Johns Fruit Cake       | Condiments
              1 | Johns Fruit Cake       | Confections
              1 | Johns Fruit Cake       | Dairy Products
              1 | Johns Fruit Cake       | Grains/Cereals
              1 | Johns Fruit Cake       | Meat/Poultry
              1 | Johns Fruit Cake       | Produce
              1 | Johns Fruit Cake       | Seafood
              2 | Marys Healthy Mix      | Beverages
              2 | Marys Healthy Mix      | Condiments
              2 | Marys Healthy Mix      | Confections
              2 | Marys Healthy Mix      | Dairy Products
              2 | Marys Healthy Mix      | Grains/Cereals
              2 | Marys Healthy Mix      | Meat/Poultry
              2 | Marys Healthy Mix      | Produce
              2 | Marys Healthy Mix      | Seafood
              3 | Peters Scary Stuff     | Beverages
              3 | Peters Scary Stuff     | Condiments
              3 | Peters Scary Stuff     | Confections
              3 | Peters Scary Stuff     | Dairy Products
              3 | Peters Scary Stuff     | Grains/Cereals
              3 | Peters Scary Stuff     | Meat/Poultry
              3 | Peters Scary Stuff     | Produce
              3 | Peters Scary Stuff     | Seafood
              4 | Jims Secret Recipe     | Beverages
              4 | Jims Secret Recipe     | Condiments
              4 | Jims Secret Recipe     | Confections
              4 | Jims Secret Recipe     | Dairy Products
              4 | Jims Secret Recipe     | Grains/Cereals
              4 | Jims Secret Recipe     | Meat/Poultry
              4 | Jims Secret Recipe     | Produce
              4 | Jims Secret Recipe     | Seafood
              5 | Elisabeths Best Apples | Beverages
              5 | Elisabeths Best Apples | Condiments
              5 | Elisabeths Best Apples | Confections
              5 | Elisabeths Best Apples | Dairy Products
              5 | Elisabeths Best Apples | Grains/Cereals
              5 | Elisabeths Best Apples | Meat/Poultry
              5 | Elisabeths Best Apples | Produce
              5 | Elisabeths Best Apples | Seafood
              6 | Janes Favorite Cheese  | Beverages
              6 | Janes Favorite Cheese  | Condiments
              6 | Janes Favorite Cheese  | Confections
              6 | Janes Favorite Cheese  | Dairy Products
              6 | Janes Favorite Cheese  | Grains/Cereals
              6 | Janes Favorite Cheese  | Meat/Poultry
              6 | Janes Favorite Cheese  | Produce
              6 | Janes Favorite Cheese  | Seafood
              7 | Billys Home Made Pizza | Beverages
              7 | Billys Home Made Pizza | Condiments
              7 | Billys Home Made Pizza | Confections
              7 | Billys Home Made Pizza | Dairy Products
              7 | Billys Home Made Pizza | Grains/Cereals
              7 | Billys Home Made Pizza | Meat/Poultry
              7 | Billys Home Made Pizza | Produce
              7 | Billys Home Made Pizza | Seafood
              8 | Ellas Special Salmon   | Beverages
              8 | Ellas Special Salmon   | Condiments
              8 | Ellas Special Salmon   | Confections
              8 | Ellas Special Salmon   | Dairy Products
              8 | Ellas Special Salmon   | Grains/Cereals
              8 | Ellas Special Salmon   | Meat/Poultry
              8 | Ellas Special Salmon   | Produce
              8 | Ellas Special Salmon   | Seafood
              9 | Roberts Rich Spaghetti | Beverages
              9 | Roberts Rich Spaghetti | Condiments
              9 | Roberts Rich Spaghetti | Confections
              9 | Roberts Rich Spaghetti | Dairy Products
              9 | Roberts Rich Spaghetti | Grains/Cereals
              9 | Roberts Rich Spaghetti | Meat/Poultry
              9 | Roberts Rich Spaghetti | Produce
              9 | Roberts Rich Spaghetti | Seafood
             10 | Mias Popular Ice       | Beverages
             10 | Mias Popular Ice       | Condiments
             10 | Mias Popular Ice       | Confections
             10 | Mias Popular Ice       | Dairy Products
             10 | Mias Popular Ice       | Grains/Cereals
             10 | Mias Popular Ice       | Meat/Poultry
             10 | Mias Popular Ice       | Produce
             10 | Mias Popular Ice       | Seafood
(80 rows)
```