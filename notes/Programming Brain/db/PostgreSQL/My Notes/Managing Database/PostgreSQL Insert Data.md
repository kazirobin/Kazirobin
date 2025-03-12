# PostgreSQL Insert Data

To insert data into a table in PostgreSQL, we use the `INSERT INTO` statement. The following SQL statement will insert one row of data into the `cars` table you created in the previous chapter.

```bash
INSERT INTO cars (brand, model, year)
VALUES ('Ford', 'Mustang', 1964);
```

The SQL Shell application will return the following:

```bash
INSERT 0 1
```

Which means that `1` row was inserted.

Don't think about the `0`, for now, just accept that it represents something else and will always be `0`.

## SQL Statement Explained

As you can see in the SQL statement above, string values must be written with apostrophes.

Numeric values can be written without apostrophes, but you can include them if you want.

## Display Table

To check the result we can display the table with this SQL statement:

```bash
SELECT * FROM cars;
```

Which will return this result:

```bash
 brand |  model  | year
-------+---------+------
 Ford  | Mustang | 1964
(1 row)
```

## Insert Multiple Rows

To insert multiple rows of data, we use the same `INSERT INTO` statement, but with multiple values:

```bash
INSERT INTO cars (brand, model, year)
VALUES
  ('Volvo', 'p1800', 1968),
  ('BMW', 'M1', 1978),
  ('Toyota', 'Celica', 1975);
```

The SQL Shell application will return the following:

```bash
INSERT 0 3
```

Which means `3` rows were successfully inserted.