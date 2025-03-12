# PostgreSQL ASCII()

The PostgreSQL `ASCII()` function returns an ASCII code value of a character. In the case of UTF-8, the `ASCII()` function returns the Unicode code point of the character.

The following example uses the `ASCII()` function to get the ASCII code values of the character `A` and `a`:

```bash
SELECT
    ASCII( 'A' ),
    ASCII( 'a' );
```