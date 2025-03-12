# PostgreSQL LENGTH()

The PostgreSQL `LENGTH()` function returns the number of characters in a string.

Here’s the basic syntax for the `LENGTH()` function:

```bash
LENGTH(string);
```

The `LENGTH()` function accepts a string as a parameter. It can be any of the following [data types](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-data-types/):

- character or char
- character varying or varchar
- text

The `LENGTH()` function returns an integer that represents the number of characters in the string. It returns NULL if the string is null.

PostgreSQL provides the `CHAR_LENGTH()` and `CHARACTER_LENGTH()` functions that provide the same functionality as the `LENGTH()` function.

Let’s explore some examples of using the `LENGTH()` function.

The following example uses the `LENGTH()` function to get the length of a string:

```bash
SELECT 
  LENGTH ('PostgreSQL Tutorial');
```

Output:

```bash
 length
--------
     19
(1 row)
```

If you pass NULL to the `LENGTH()` function, it returns NULL.

```bash
SELECT 
  LENGTH (NULL);
```

Output:

```bash
 length
--------
   null
(1 row)
```

Using the PostgreSQL LENGTH() function with table data example

We’ll use the `customer` table from the sample database:

The following example uses the `LENGTH()` function to retrieve the first names and the number of characters of first names from the `customer` table:

```bash
SELECT 
  first_name, 
  LENGTH (first_name) len 
FROM 
  customer 
ORDER BY 
  len;
```

Output:

```bash
 first_name  | len
-------------+-----
 Jo          |   2
 Sam         |   3
 Roy         |   3
 Eva         |   3
 Don         |   3
 Dan         |   3
...
```