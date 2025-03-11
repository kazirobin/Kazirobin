# PostgreSQL FORMAT()

The `FORMAT()` function allows you to format strings based on a template. 

Here’s the basic syntax of the `FORMAT()` function:

```bash
FORMAT(format_string, value1, value2, ...)
```

In this syntax:

- `format_string`: This is the input string that you want to format.
- `value1`, `value2`, …: These are values to be inserted into placeholders in the `format_string`.

The `FORMAT()` function returns a formatted string. The `FORMAT()` function can be useful for creating dynamic strings with placeholders for variables.

## Format Specifier

The following shows the syntax of the format specifier:

```bash
%[position][flags][width]type
```

A format specifier starts with `%` character and include three optional components `position`, `flags`, `width` and a required component `type`.

### Position

The `position` specifies which argument to be inserted in the result string. The `position` is in the form `n$` where `n` is the argument index. The first argument starts from 1.

If you omit the `position` component, the default is the next argument in the list.

### Flags

The `flags` can accept a minus sign (-) that instructs the format specifier’s output to be left-justified.

The `flags` component only takes effect when the `width` field is specified.

### Width

The optional `width` field specifies the minimum number of characters to use for displaying the format specifier’s output. The result string can be padded left or right with the spaces needed to fill the `width`.

If the `width` is too small, the output will be displayed as-is without any truncation.

The `width` can be one of the following values:

- A positive integer.
- An asterisk (*) to use the next function argument as the width.
- A string of the form `n$` to use the `nth` function argument as the width.

### Type

`type` is the type of format conversion to use to produce the format specifier’s output.

The permitted values for type argument are as follows:

- `s` formats the argument value as a string. NULL is treated as an empty string.
- `I` treats the argument value as an SQL identifier.
- `L` quotes the argument value as an SQL literal.

We often use `I` and `L` for constructing dynamic SQL statements.
If you want to include `%` in the result string, use double percentages `%%`

Let’s explore some examples of using the `FORMAT()` function.

The following statement uses the `FORMAT()` function to format a string:

```bash
SELECT FORMAT('Hello, %s','PostgreSQL');
```

Output:

```bash
'Hello, PostgreSQL'
```

In this example, the function replaces the `%s` with the `'PostgreSQL'` string argument.