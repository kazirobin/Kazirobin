# PostgreSQL UPPER()

The `UPPER()` function converts a string to uppercase based on the rules of the database’s locale.

Here’s the syntax of the `UPPER()` function:

```bash
UPPER(text)
```

In this syntax, `text` is the input string that you want to convert to uppercase. Its type can be `CHAR`, `VARCHAR`, or `TEXT`.

The `UPPER()` function returns a new string with all letters converted to uppercase. The `UPPER()` function returns `NULL` if the `text` is `NULL`.

Let’s take some examples of using the `UPPER()` function.

The following example uses the `UPPER()` function to convert the string `PostgreSQL` to uppercase:

```bash
SELECT UPPER('PostgreSQL');
```

Output:

```bash
   upper
------------
 POSTGRESQL
(1 row)
```

Using PostgreSQL UPPER() function with table data

We’ll use the `customer` table from the sample database. The following example uses the `UPPER()` function to convert the first names of customers to uppercase:

```bash
SELECT 
  UPPER(first_name) 
FROM 
  customer 
ORDER BY 
  first_name;
```

Output:

```bash
    upper
-------------
 AARON
 ADAM
 ADRIAN
 AGNES
 ALAN
...
```

Using PostgreSQL UPPER() function in the WHERE clause

The following example uses the `UPPER()` function in the `WHERE` clause to find customers by last names, comparing them with the input string in uppercase:

```bash
SELECT 
  first_name, 
  last_name 
FROM 
  customer 
WHERE 
  UPPER(last_name) = 'BARNETT';
```

Output:

```bash
 first_name | last_name
------------+-----------
 Carole     | Barnett
(1 row)
```