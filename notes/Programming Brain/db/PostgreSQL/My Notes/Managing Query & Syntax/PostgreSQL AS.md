# PostgreSQL AS

SQL aliases are used to give a table, or a column in a table, a temporary name. Aliases are often used to make column names more readable. An alias only exists for the duration of that query. An alias is created with the `AS` keyword.

Using aliases for columns:

```bash
SELECT customer_id AS id
FROM customers;
```

## AS is Optional

Actually, you can skip the `AS` keyword and get the same result:

Same result without `AS`:

```bash
SELECT customer_id id
FROM customers;
```

## Concatenate Columns

The `AS` keyword is often used when two or more fields are concatenated into one. To concatenate two fields use `||`.

Concatenate two fields and call them `product`:

```bash
SELECT product_name || unit AS product
FROM products;
```

**Note:** In the result of the example above we are missing a space between product_name and unit. To add a space when concatenating, use `|| ' ' ||`.

Concatenate, with space:

```bash
SELECT product_name || ' ' || unit AS product
FROM products;
```

## Using Aliases With a Space Character

If you want your alias to contain one or more spaces, like "`My Great Products`", surround your alias with double quotes.

Surround your alias with double quotes:

```bash
SELECT product_name AS "My Great Products"
FROM products;
```