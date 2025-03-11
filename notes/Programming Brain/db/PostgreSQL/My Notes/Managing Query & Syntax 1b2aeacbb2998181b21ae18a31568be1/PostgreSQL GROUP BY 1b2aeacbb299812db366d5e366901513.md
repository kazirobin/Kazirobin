# PostgreSQL GROUP BY

The `GROUP BY` clause groups rows that have the same values into summary rows, like "find the number of customers in each country".

The `GROUP BY` clause is often used with aggregate functions like `COUNT()`, `MAX()`, `MIN()`, `SUM()`, `AVG()` to group the result-set by one or more columns.

Lists the number of customers in each country:

```bash
SELECT COUNT(customer_id), country
FROM customers
GROUP BY country;
```

## GROUP BY With JOIN

The following SQL statement lists the number of orders made by each customer:

```bash
SELECT customers.customer_name, COUNT(orders.order_id)
FROM orders
LEFT JOIN customers ON orders.customer_id = customers.customer_id
GROUP BY customer_name;
```