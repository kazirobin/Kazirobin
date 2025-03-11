# PostgreSQL LTRIM()

The `LTRIM()` function allows you to remove specified characters from the beginning of a string.

Here’s the syntax of the `LTRIM()` function:

```bash
LTRIM(string, character)
```

In this syntax:

- `string` is the input string that you want to remove characters.
- `character` specifies the characters you want to remove from the beginning of the `string`. The `character` parameter is optional. It defaults to space.

The `LTRIM()` function returns the string with all leading characters removed. To remove both leading and trailing characters from a string, you use the TRIM() function. To remove the trailing characters from a string, you use the RTRIM() function.

Let’s explore some examples of using the `LTRIM()` function.

## Basic PostgreSQL LTRIM() function example

The following example uses the `LTRIM()` function to remove the `#` from the beginning of the string `#postgres`:

```bash
SELECT LTRIM('#postgres', '#');
```

Output:

```bash
  ltrim
----------
 postgres
(1 row)
```

## Using the PostgreSQL LTRIM() function to remove leading spaces

The following example uses the `LTRIM()` function to remove all the spaces from the string `' PostgreSQL'`:

```bash
SELECT LTRIM('   PostgreSQL');
```

Output:

```bash
   ltrim
------------
 PostgreSQL
(1 row)
```

Since the default of the second argument of the `LTRIM()` function is space, we don’t need to specify it.

## Using the LTRIM() function with table data example

First, create a new table called `articles` and insert some rows into it:

```bash
CREATE TABLE articles(
   id SERIAL PRIMARY KEY,
   title VARCHAR(255) NOT NULL
);

INSERT INTO articles(title)
VALUES
   ('   Mastering PostgreSQL string functions'),
   (' PostgreSQL LTRIM() function')
RETURNING *;
```

Output:

```bash
 id |                  title
----+------------------------------------------
  1 |    Mastering PostgreSQL string functions
  2 |  PostgreSQL LTRIM() function
(2 rows)
```

Second, update the titles by removing the leading spaces using the `LTRIM()` function:

```bash
UPDATE articles
SET title = LTRIM(title);
```

Output:

```bash
UPDATE 2
```

The output indicates that two rows were updated.

Third, verify the updates:

```bash
SELECT * FROM articles;
```

Output:

```bash
 id |                 title
----+---------------------------------------
  1 | Mastering PostgreSQL string functions
  2 | PostgreSQL LTRIM() function
(2 rows)
```