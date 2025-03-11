# PostgreSQL CONCAT_WS()

The PostgreSQL `CONCAT_WS()` function allows you to concatenate multiple strings into a single string separated by a specified separator.

Here’s the basic syntax of the `CONCAT_WS` function:

```bash
CONCAT_WS(separator, string1, string2, string3, ...)
```

In this syntax:

- `separator`: Specify the separator that you want to separate the strings. The `separator` should not be `NULL`.
- `string1`, `string2`, `string3`, ..: These are strings that you want to concatenate. If any string is NULL, it is ignored by the function.

The `CONCAT_WS` returns a single string that combines the `string1`, `string2`, `string3`… separated by the separator. If the separator is `NULL`, the `CONCAT_WS` will return `NULL`.

Let’s take some examples of using the `CONCAT_WS()` function.

The following example uses the `CONCAT_WS()` function to concatenate two strings with a space:

```bash
SELECT CONCAT_WS(' ', 'PostgreSQL', 'Tutorial') title;
```

Output:

```bash
        title
---------------------
 PostgreSQL Tutorial
(1 row)
```

In this example, we use the `CONCAT_WS()` function to concatenate the strings `'PostgreSQL'` and `'Tutorial'` with a space separator. The result string is `'PostgreSQL Tutorial'`.

## CONCAT_WS() With Table Data

We’ll use the `customer` table from the sample database:

The following example uses the `CONCAT_WS()` to concatenate values from the `first_name` and `last_name` columns of the `customer` table using a space as a separator:

```bash
SELECT 
  CONCAT_WS(' ', first_name, last_name) full_name 
FROM 
  customer 
ORDER BY 
  first_name;
```

Output:

```bash
       full_name
-----------------------
 Aaron Selby
 Adam Gooch
 Adrian Clary
 Agnes Bishop
...
```