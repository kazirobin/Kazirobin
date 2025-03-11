# PostgreSQL POSITION()

The PostgreSQL `POSITION()` function returns the location of the first instance of a substring within a string.

The following illustrates the syntax of the `POSITION()` function:

```bash
POSITION(substring IN string)
```

The `POSITION()` function requires two arguments:

### 1) SubString

The substring argument is the string that you want to locate.

### 2) String

The `string` argument is the string for which the substring is searched.

The `POSITION()` function returns an integer representing the location of the first instance of the substring within the input string. The `POSITION()` function returns zero (0) if the substring is not found in the string. It returns NULL if either `substring` or `string` argument is null.

The following example returns the position of the `'Tutorial'` in the string `'PostgreSQL Tutorial'`:

```bash
SELECT POSITION('Tutorial' IN 'PostgreSQL Tutorial');
```

The result is as follows:

```bash
position
----------
       12
(1 row)
```

**Note:** that the `POSITION()` function searches for the substring case-insensitively.

See the following example:

```bash
SELECT POSITION('tutorial' IN 'PostgreSQL Tutorial');
```

It returns zero (0), indicating that the string `tutorial` does not exist in the string `'PostgreSQL Tutorial'`.

The following example uses the `POSITION()` function to locate the first string `'fateful'` in the `description` column of the `film` table from the sample database:

```bash
SELECT 
  POSITION('Fateful' in description ), 
  description 
FROM 
  film 
WHERE 
  POSITION('Fateful' in description ) > 0;
```

Output:

```bash
 position |                                                   description
----------+-----------------------------------------------------------------------------------------------------------------
        3 | A Fateful Reflection of a Moose And a Husband who must Overcome a Monkey in Nigeria
        3 | A Fateful Yarn of a Lumberjack And a Feminist who must Conquer a Student in A Jet Boat
        3 | A Fateful Yarn of a Womanizer And a Feminist who must Succumb a Database Administrator in Ancient India
        3 | A Fateful Display of a Womanizer And a Mad Scientist who must Outgun a A Shark in Soviet Georgia
...
```