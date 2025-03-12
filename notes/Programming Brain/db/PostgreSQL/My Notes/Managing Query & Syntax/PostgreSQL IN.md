# PostgreSQL IN

The `IN` operator allows you to specify a list of possible values in the WHERE clause. 

## IN

The `IN` operator is a shorthand for multiple `OR` conditions.

Return all customers from 'Germany', France' or 'UK':

```bash
SELECT * FROM customers
WHERE country IN ('Germany', 'France', 'UK');
```

## NOT IN

By using the `NOT` keyword in front of the `IN` operator, you return all records that are NOT any of the values in the list.

Return all customers that are NOT from 'Germany', France' or 'UK':

```bash
SELECT * FROM customers
WHERE country NOT IN ('Germany', 'France', 'UK');
```

## IN (SELECT)

You can also use a `SELECT` statement inside the parenthesis to return all records that are in the result of the `SELECT` statement.

Return all customers that have an order in the `orders` table:

```bash
SELECT * FROM customers
WHERE customer_id IN (SELECT customer_id FROM orders);
```

## NOT IN (SELECT)

The result in the example above returned 89 records, that means that there are 2 customers that haven't placed any orders. Let us check if that is correct, by using the `NOT IN` operator.

Return all customers that have NOT placed any orders in the `orders` table:

```bash
SELECT * FROM customers
WHERE customer_id NOT IN (SELECT customer_id FROM orders);
```