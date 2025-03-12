# PostgreSQL LEFT()

The PostgreSQL `LEFT()` function returns the first `n` characters in the string.

The following illustrates the syntax of the PostgreSQL `LEFT()` function:

```bash
LEFT(string, n) 
```

The PostgreSQL `LEFT()` function requires two arguments:

`String` is a string from which a number of the leftmost characters returned.

**`n`** is an integer that specifies the number of left-most characters in the string should be returned.

If `n` is negative, the `LEFT()` function returns the leftmost characters in the string but last `|n|` (absolute) characters.

Let’s look at some examples of using the `LEFT()` function.

The following example shows how to get the first character of a string `'ABC'`:

```bash
SELECT LEFT('ABC',1);
```

The result is

```bash
 left
------
 A
(1 row)
```

To get the first two characters of the string ‘ABC’, you use 2 instead of 1 for the `n` argument:

```bash
SELECT LEFT('ABC',2);
```

Here is the result:

```bash
 left
------
 AB
(1 row)
```

The following statement demonstrates how to use a negative integer:

```bash
SELECT LEFT('ABC',-2);
```

In this example, n is -2, therefore, the `LEFT()` function return all character except the last 2 characters, which results in:

```bash
 left
------
 A
(1 row)
```