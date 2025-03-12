# PostgreSQL RPAD()

The `RPAD()` function allows you to extend a string to a length by appending specified characters.

Here’s the basic syntax of the `RPAD()` function:

```bash
RPAD(string, length, fill)
```

In this syntax:

- `string`: The input string that you want to extend.
- `length`: The desired length of the string after padding.
- `fill`: The character or string used for padding.

The `RPAD()` function returns the string, right-padded with the string `fill` to a length of `length` characters.

If the length of the `string` is greater than the desired `length`, the `RPAD()` function truncates the `string` to the `length` characters.

If any argument `string`, `length`, or `fill` is `NULL`, the `RPAD()` function returns [`NULL`](https://www.mysqltutorial.org/mysql-basics/mysql-null/).

The `RPAD()` function can be particularly useful when you need to format text with a consistent length, align text in columns, or prepare data for display.

Let’s explore some examples of using the PostgreSQL `RPAD()` function.

## Basic PostgreSQL RPAD() function

The following example uses the `RPAD()` function to extend a string by filling zeros (‘0’) to make it six characters long:

```bash
SELECT RPAD('123', 6, '0');
```

Output:

```bash
  rpad
--------
 123000
(1 row)
```

## Using the RPAD() function with the table data example

We’ll use the `film` table from the sample database:

The following example uses the `RPAD()` function to right-pad the titles from the `film` table with the character ‘.’ to make it 50 characters long:

```bash
SELECT 
  RPAD(title, 50, '.') 
FROM 
  film;
```

Output:

```bash
                        rpad
----------------------------------------------------
 Chamber Italian...................................
 Grosse Wonderful..................................
 Airport Pollock...................................
 Bright Encounters.................................
 Academy Dinosaur..................................
...
```

## Using the RPAD() function to truncate strings

The following example uses the `RPAD()` function to truncate the titles if their lengths are more than 10 characters:

```bash
SELECT 
  title, RPAD(title, 10, '') result
FROM 
  film;
```

Output:

```bash
            title            |   result
-----------------------------+------------
 Chamber Italian             | Chamber It
 Grosse Wonderful            | Grosse Won
 Airport Pollock             | Airport Po
 Bright Encounters           | Bright Enc
 Academy Dinosaur            | Academy Di
 Ace Goldfinger              | Ace Goldfi
...
```