# PostgreSQL LOWER()

The `LOWER()` function converts a string to lowercase based on the rules of the database’s locale.

Here’s the syntax of the `LOWER()` function:

```bash
LOWER(text)
```

In this syntax, text is the input string that you want to convert. Its type can be `CHAR`, `VARCHAR`, or `TEXT`.

The `LOWER()` function returns a new string with all letters converted to lowercase.

If the text is `NULL`, the `LOWER()` function returns `NULL`.

Let’s explore some examples of using the `LOWER()` function.

The following example uses the `LOWER()` function to convert the string PostgreSQL to lowercase:

```bash
SELECT LOWER('PostgreSQL');
```

Output:

```bash
   lower
------------
 postgresql
(1 row)
```

Using PostgreSQL LOWER() function with table data

We’ll use the `customer` table from the sample database. The following example uses the `LOWER()` function to convert the first names of customers to lowercase:

```bash
SELECT 
  LOWER(first_name) 
FROM 
  customer 
ORDER BY 
  first_name;
```

Output:

```bash
    lower
-------------
 aaron
 adam
 adrian
 agnes
 alan
...
```

Using PostgreSQL LOWER() function in the WHERE clause

The following example uses the `LOWER()` function in the `WHERE` clause to find customers by last names, comparing them with the input string in lowercase:

```bash
SELECT 
  first_name, 
  last_name 
FROM 
  customer 
WHERE 
  LOWER(last_name) = 'barnett';
```

Output:

```bash
 first_name | last_name
------------+-----------
 Carole     | Barnett
(1 row)
```