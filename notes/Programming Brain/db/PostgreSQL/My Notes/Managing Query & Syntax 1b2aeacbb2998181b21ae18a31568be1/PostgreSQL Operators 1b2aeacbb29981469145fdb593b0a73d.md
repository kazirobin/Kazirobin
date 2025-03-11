# PostgreSQL Operators

We can operate with different operators in the `WHERE` clause:

| **=** | Equal to |
| --- | --- |
| **<** | Less than |
| **>** | Greater than |
| **<=** | Less than or equal to |
| **>=** | Greater than or equal to |
| **<>** | Not equal to |
| **!=** | Not equal to |
| **LIKE** | Check if a value matches a pattern (case sensitive) |
| **ILIKE** | Check if a value matches a pattern (case insensitive) |
| **AND** | Logical AND |
| **OR** | Check if a value is between a range of values |
| **BETWEEN** | Check if a value is between a range of values |
| **IS NULL** | Check if a value is NULL |
| **NOT** | Makes a negative result e.g. NOT LIKE, NOT IN, NOT BETWEEN
 |

## Equal To

The `=` operator is used when you want to return all records where a column is equal to a specified value:

Return all records where the brand is 'Volvo':

```bash
SELECT * FROM cars WHERE brand = 'Volvo';
```

## Less Than

The `<` operator is used when you want to return all records where a column is less than a specified value.

Return all records where the year is less than 1975:

```bash
SELECT * FROM cars WHERE year < 1975;
```

## Greater Than

The `>` operator is used when you want to return all records where a columns is greater than a specified value.

Return all records where the year is greater than 1975:

```bash
SELECT * FROM cars WHERE year > 1975;
```

## Less Than or Equal To

The `<=` operator is used when you want to return all records where a column is less than, or equal to, a specified value.

Return all records where the year is less than or equal to 1975:

```bash
SELECT * FROM cars WHERE year <= 1975;
```

## Greater Than or Equal to

The `>=` operator is used when you want to return all records where a columns is greater than, or equal to, a specified value.

Return all records where the year is greater than or equal 1975:

```bash
SELECT * FROM cars WHERE year >= 1975;
```

## Not Equal To

The `<>` operator is used when you want to return all records where a column is NOT equal to a specified value:

Return all records where the brand is NOT 'Volvo':

```bash
SELECT * FROM cars WHERE brand <> 'Volvo';
```

You will get the same result with the `!=` operator:

```bash
SELECT * FROM cars WHERE brand != 'Volvo';
```

## LIKE

The `LIKE` operator is used when you want to return all records where a column is equal to a specified pattern.

The pattern can be an absolute value like 'Volvo', or with a wildcard that has a special meaning.

There are two wildcards often used in conjunction with the LIKE operator:

- The percent sign `%`, represents zero, one, or multiple characters.
- The underscore sign `_`, represents one single character.

Return all records where the model STARTS with a capital 'M':

```bash
SELECT * FROM cars WHERE model LIKE 'M%';
```

The `LIKE` operator is case sensitive.

## ILIKE

Same as the `LIKE` operator, but `ILIKE` is case insensitive.

Return all records where the model start with a 'm':

```bash
SELECT * FROM cars WHERE model ILIKE 'm%';
```

## AND

The logical `AND` operator is used when you want to check more that one condition:

Return all records where the brand is 'Volvo' and the year is 1968:

```bash
SELECT * FROM cars WHERE brand = 'Volvo' AND year = 1968;
```

## OR

The logical `OR` operator is used when you can accept that only one of many conditions is true:

Return all records where the brand is 'Volvo' OR the year is 1975:

```bash
SELECT * FROM cars WHERE brand = 'Volvo' OR year = 1975;
```

## IN

The `IN` operator is used when a column's value matches any of the values in a list:

Return all records where the brand is present in this list: ('Volvo', 'Mercedes', 'Ford'):

```bash
SELECT * FROM cars WHERE brand IN ('Volvo', 'Mercedes', 'Ford');
```

## BETWEEN

The `BETWEEN` operator is used to check if a column's value is between a specified range of values:

Return all records where the year is between 1970 and 1980:

```bash
SELECT * FROM cars WHERE year BETWEEN 1970 AND 1980;
```

The `BETWEEN` operator includes the `*from*` and `*to*` values, meaning that in the above example, the result would include cars made in 1970 and 1980 as well.

## IS NULL

The `IS NULL` operator is used to check if a column's value is NULL:

Return all records where the model is NULL:

```bash
SELECT * FROM cars WHERE model IS NULL;
```

## NOT

The `NOT` operator can be used together with `LIKE`, `ILIKE`, `IN`, `BETWEEN`, and `NULL` operators to reverse the truth of the operator.

Return all records where the brand does NOT start with a capital 'B' (case sensitive):

```bash
# NOT LIKE

SELECT * FROM cars WHERE brand NOT LIKE 'B%';
```

Return all records where the brand does NOT start with a 'b' (case insensitive):

```bash
# NOT ILIKE

SELECT * FROM cars WHERE brand NOT LIKE 'b%';
```

Return all records where the brand is NOT present in this list: ('Volvo', 'Mercedes', 'Ford'):

```bash
# NOT IN

SELECT * FROM cars WHERE brand NOT IN ('Volvo', 'Mercedes', 'Ford');
```

Return all records where the year is NOT between 1970 and 1980:

```bash
# NOT BETWEEN

SELECT * FROM cars WHERE year NOT BETWEEN 1970 AND 1980;
```

The `NOT BETWEEN` operator excludes the `*from*` and `*to*` values, meaning that in the above example, the result would not include cars made in 1970 and 1980.

Return all records where the model is NOT null:

```bash
# IS NOT NULL

SELECT * FROM cars WHERE model IS NOT NULL;
```