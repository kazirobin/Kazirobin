# PostgreSQL CHR()

The PostgreSQL `CHR()` function converts an integer ASCII code to a character or a Unicode code point to a UTF8 character.

The `CHR()` function requires one argument. The num argument is an integer that is converted to the corresponding ASCII code. It could be a Unicode code point which is converted to a UTF8 character.

The following example shows how to use the `CHR()` function to get the characters whose ASCII code value is 65 and 97:

```bash
SELECT
    CHR(65),
    CHR(97);
```

The query returns character A for 65 and a for 97: