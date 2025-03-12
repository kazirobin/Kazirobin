# PostgreSQL HAVING

The `HAVING` clause was added to SQL because the `WHERE` clause cannot be used with aggregate functions.

Aggregate functions are often used with `GROUP BY` clauses, and by adding `HAVING` we can write condition like we do with `WHERE` clauses.

List only countries that are represented more than 5 times:

```bash
SELECT COUNT(customer_id), country
FROM customers
GROUP BY country
HAVING COUNT(customer_id) > 5;
```

## More HAVING Examples

The following SQL statement lists only orders with a total price of 400$ or more:

```bash
SELECT order_details.order_id, SUM(products.price)
FROM order_details
LEFT JOIN products ON order_details.product_id = products.product_id
GROUP BY order_id
HAVING SUM(products.price) > 400.00;
```

Lists customers that have ordered for 1000$ or more:

```bash
SELECT customers.customer_name, SUM(products.price)
FROM order_details
LEFT JOIN products ON order_details.product_id = products.product_id
LEFT JOIN orders ON order_details.order_id = orders.order_id
LEFT JOIN customers ON orders.customer_id = customers.customer_id
GROUP BY customer_name
HAVING SUM(products.price) > 1000.00;
```