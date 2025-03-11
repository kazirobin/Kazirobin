# PostgreSQL MIN & MAX

The `MIN()` function returns the smallest value of the selected column. And The `MAX()` function returns the largest value of the selected column.

### MIN

Return the lowest price in the `products` table:

```bash
SELECT MIN(price) FROM products;
```

### MAX

Return the highest price in the `products` table:

```bash
SELECT MAX(price) FROM products;
```

### Set Column Name

When you use `MIN()` or `MAX()`, the returned column will be named `min` or `max` by default. To give the column a new name, use the `AS` keyword.

Return the lowest price, and new name the column `lowest_price`:

```bash
SELECT MIN(price) AS lowest_price FROM products;
```