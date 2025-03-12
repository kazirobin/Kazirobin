# Logical Operators

Logical operators perform logical operations and return a boolean value, either `true` or `false`.

```jsx
const x = 5, y = 3;
(x < 6) && (y < 5); // true
```

Here, `&&` is the logical operator AND. Since both `x < 6` and `y < 5` are `true`, the result is `true`.

| Operator | Description | Example |
| --- | --- | --- |
| && | **Logical AND**: `true` if both the operands are `true`, else returns `false` | x  &&  y |
| | | | **Logical OR**: `true` if either of the operands is `true`; returns false if both are `false` | x  | |  y |
| ! | **Logical NOT**: `true` if the operand is `false` and vice-versa. | ! x |