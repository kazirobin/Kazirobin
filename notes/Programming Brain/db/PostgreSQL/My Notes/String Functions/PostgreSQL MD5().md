# PostgreSQL MD5()

The PostgreSQL `MD5()` function calculates the MD5 hash of a string and returns the result in hexadecimal.

The following illustrates the syntax of the `MD5()` function:

```bash
MD5(string)
```

The `MD5()` function accepts one argument. The `string` argument is the string of which the MD5 hash is calculated. The `MD5()` function returns a string in `TEXT` data type.

The following example shows how to use the `MD5()` function to return the MD5 hash of the message `'PostgreSQL MD5'`:

```bash
SELECT MD5('PostgreSQL MD5');
```

The result is:

```bash
        md5
----------------------------------
 f78fdb18bf39b23d42313edfaf7e0a44
(1 row)
```