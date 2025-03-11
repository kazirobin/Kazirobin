# PostgreSQL TRIM()

The `TRIM()` function allows you to remove specified prefixes or suffixes (or both) from a string.

Here’s the basic syntax of the `TRIM()` function:

```bash
TRIM([LEADING | TRAILING | BOTH] trim_character 
FROM source_string)
```

In this syntax:

- `source_string`: Specify the string that you want to remove specified characters.
- `trim_character`: Specify the trim characters.
- `LEADING`: This option instructs the function to remove the leading occurrences of the specified trim character.
- `TRAILING`: This option instructs the function to remove trailing occurrences of the specified trim character.
- `BOTH`: This option instructs the function to remove both leading and trailing occurrences of the specified trim character.

The `TRIM()` function can be very useful when you want to clean up strings.

To remove specific characters from the beginning of a string, you use the LTRIM() function. To remove specific characters from the end of a string, you can use the RTRIM() function.

Let’s explore some examples of using the `TRIM()` function.

## Basic PostgreSQL TRIM() function example

The following example uses the `TRIM()` function to remove leading and trailing spaces from the string `' PostgreSQL '`:

```bash
SELECT TRIM('   PostgreSQL   ') AS trimmed_string;
```

Output:

```bash
 trimmed_string
----------------
 PostgreSQL
(1 row)
```

The output is a string without leading and trailing spaces.

## Using the PostgreSQL TRIM() function to remove specific characters

The following example uses the `TRIM()` function to remove leading and trailing hash symbols (`#`) from the string `'##PostgreSQL##'`:

```bash
SELECT TRIM('#' FROM '##PostgreSQL##') AS trimmed_string;
```

Output:

```bash
 trimmed_string
----------------
 PostgreSQL
(1 row)
```

## Using the TRIM() function to remove specific characters by specifying the trim location

The following example uses the PostgreSQL `TRIM()` function to remove leading, trailing, and both leading and trailing zeros from the string `'0000123450'`:

```bash
SELECT TRIM(LEADING '0' FROM '000123450') AS trimmed_string_leading,
       TRIM(TRAILING '0' FROM '000123450') AS trimmed_string_trailing,
       TRIM(BOTH '0' FROM '000123450') AS trimmed_string_both;
```

Output:

```bash
 trimmed_string_leading | trimmed_string_trailing | trimmed_string_both
------------------------+-------------------------+---------------------
 123450                 | 00012345                | 12345
(1 row)
```

## Using the TRIM() function with table data

First, create a table called `todo` and insert some sample data:

```bash
CREATE TABLE todo(
  id SERIAL PRIMARY KEY, 
  title VARCHAR(255) NOT NULL, 
  completed BOOL NOT NULL DEFAULT false
);

INSERT INTO todo(title) 
VALUES 
  ('   Learn PostgreSQL   '), 
  ('Build an App   ') 
RETURNING *;
```

Output:

```bash
 id |         title          | completed
----+------------------------+-----------
  1 |    Learn PostgreSQL    | f
  2 | Build an App           | f
(2 rows)
```

Second, remove the leading and trailing spaces from the `title` column using the `TRIM()` function:

```bash
UPDATE todo
SET title = TRIM(title);
```

Output:

```bash
UPDATE 2
```

Third, verify the updates:

```bash
SELECT * FROM todo;
```

Output:

```bash
 id |      title       | completed
----+------------------+-----------
  1 | Learn PostgreSQL | f
  2 | Build an App     | f
(2 rows)
```