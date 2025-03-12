# PostgreSQL RTRIM()

The `RTRIM()` function allows you to remove specified characters from the end of a string.

Here’s the syntax of the `RTRIM()` function:

```bash
RTRIM(string, character)
```

In this syntax:

- `string` is the input string that you want to remove characters
- `character` specifies the character you want to remove from the end of the string. The `character` parameter is optional and defaults to space.

The `RTRIM()` function returns the string with all trailing characters removed. To remove both leading and trailing characters from a string, you use the TRIM() function. To remove all the leading characters from a string, you use the LTRIM() function.

Let’s explore some examples of using the `RTRIM()` function.

## Basic PostgreSQL RTRIM() function example

The following example uses the `RTRIM()` function to remove the character `!` from the end of the string `postgres!!!`:

```bash
SELECT RTRIM('postgres!!!', '!');
```

Output:

```bash
  rtrim
----------
 postgres
(1 row)
```

## Using the PostgreSQL RTRIM() function to remove leading spaces

The following example uses the `RTRIM()` function to remove all the spaces from the end of the string `'PostgreSQL '`:

```bash
SELECT RTRIM('PostgreSQL   ');
```

Output:

```bash
   rtrim
------------
 PostgreSQL
(1 row)
```

Because the default of the second argument of the `RTRIM()` function is space, you don’t need to explicitly specify it.

## Using the RTRIM() function with table data example

First, create a new table called `tweets` and insert some rows into it:

```bash
CREATE TABLE tweets(
   id SERIAL PRIMARY KEY,
   tweet VARCHAR(120) NOT NULL
);

INSERT INTO tweets(tweet)
VALUES
   ('PostgreSQL tutorial   '),
   ('PostgreSQL RTRIM() function   ')
RETURNING *;
```

Output:

```bash
 id |             tweet
----+--------------------------------
  1 | PostgreSQL tutorial
  2 | PostgreSQL RTRIM() function
(2 rows)

INSERT 0 2
```

Second, update the tweets by removing the trailing spaces using the `RTRIM()` function:

```bash
UPDATE tweets
SET tweet = RTRIM(tweet);
```

Output:

```bash
UPDATE 2
```

The output indicates that two rows were updated.

Third, verify the updates:

```bash
SELECT * FROM tweets;
```

Output:

```bash
 id |            tweet
----+-----------------------------
  1 | PostgreSQL tutorial
  2 | PostgreSQL RTRIM() function
(2 rows)
```