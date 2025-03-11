# PostgreSQL CONCAT()

To concatenate two or more strings into a single string, you can use the string concatenation operator || as shown in the following example:

```bash
SELECT
   'John' || ' ' || 'Doe' AS full_name;
```

Output:

```bash
 full_name
-----------
 John Doe
(1 row)
```

The following statement uses the concatenation operator (`||`) to concatenate a string with `NULL`:

```bash
SELECT
   'John' || NULL result;
```

It returns `NULL`.

Since version 9.1, PostgreSQL has introduced a built-in string function called `CONCAT()` to concatenate two or more strings into one.

Here’s the basic syntax of the `CONCAT()` function:

```bash
CONCAT(string1, string2, ...)
```

The `CONCAT` function accepts a list of input strings, which can be any string type including `CHAR`, `VARCHAR`, and `TEXT`.

The `CONCAT()` function returns a new string that results from concatenating the input strings. Unlike the concatenation operator `||`, the `CONCAT` function ignores  `NULL` arguments.

Let’s take some examples of using the PostgreSQL `CONCAT()` function.

The following example uses the `CONCAT()` function to concatenate three literal strings into one:

```bash
SELECT 
  CONCAT('John', ' ', 'Doe') full_name;
```

Output:

```bash
 full_name
-----------
 John Doe
(1 row)
```

## CONCAT() With Table Data

We’ll use the `customer` table from the sample database:

The following statement uses the `CONCAT()` function to concatenate values in the `first_name`, a space, and values in the `last_name` columns of the `customer` table into a single string:

```bash
SELECT 
  CONCAT (first_name, ' ', last_name) AS full_name
FROM
  customer
ORDER BY
  full_name;
```

Output:

```bash
       full_name
-----------------------
 Aaron Selby
 Adam Gooch
 Adrian Clary
 Agnes Bishop
 Alan Kahn
...
```

## CONCAT() With NULL

First, create a table called `contacts` and insert some rows into it:

```bash
CREATE TABLE contacts (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(15)
);

INSERT INTO contacts (name, email, phone) 
VALUES
    ('John Doe', 'john@gmail.com', '123-456-7890'),
    ('Jane Smith', 'jane@example.com', NULL),
    ('Bob Johnson', 'bob@example.com', '555-1234'),
    ('Alice Brown', 'alice@example.com', NULL),
    ('Charlie Davis', 'charlie@example.com', '987-654-3210')
RETURNING *;
```

Output:

```bash
 id |     name      |        email        |    phone
----+---------------+---------------------+--------------
  1 | John Doe      | john@gmail.com      | 123-456-7890
  2 | Jane Smith    | jane@example.com    | null
  3 | Bob Johnson   | bob@example.com     | 555-1234
  4 | Alice Brown   | alice@example.com   | null
  5 | Charlie Davis | charlie@example.com | 987-654-3210
(5 rows)

INSERT 0 5
```

Second, use the `CONCAT()` function to concatenate the values in the `name`, `email`, and `phone` columns of the `contacts` table:

```bash
SELECT 
  CONCAT(name, ' ', '(', email, ')', ' ', phone) contact
FROM 
  contacts;
```

The output indicates that the `CONCAT()` function ignores `NULL`.