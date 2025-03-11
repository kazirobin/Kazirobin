# Short Circuiting Operators

In JavaScript short-circuiting, an expression is evaluated from left to right until it is confirmed that the result of the remaining conditions is not going to affect the already evaluated result. If the result is clear even before the complete evaluation of the expression, it short circuits and the result will be returned. Short circuit evaluation avoids unnecessary work and leads to efficient processing.

### Short-circuiting with the or `(||)` operator

The `||` operator will return the first truthy value of all the operands, or simply the last value if all of them are falsy.

```jsx
'' || "JavaScript"

// returns JavaScript
```

### Short-circuiting with the and `(&&)` operator

The `&&` operator will return false as soon as it gets any falsy value and will return the last true value if all the values are truthy.

```jsx
true && "JavaScript"

// returns JavaScript
```