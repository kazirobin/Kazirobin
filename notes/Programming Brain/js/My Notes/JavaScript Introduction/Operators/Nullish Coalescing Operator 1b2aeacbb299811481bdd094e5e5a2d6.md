# Nullish Coalescing Operator

The double question mark `(??)` denotes the nullish coalescing operator introduced in ES6. When its left-hand side operand is undefined or null, the nullish coalescing `(??)` operator returns its right-hand side operand. In all other cases, the logical operator returns its left-hand side operand.

The following syntax shows the basic operation of the nullish coalescing operator. There are two values that the nullish coalescing operator will accept:

```jsx
const language = null;

language ?? "JavaScript";
```

If the first value `(language)` is null or undefined, the nullish coalescing operator returns the second value `("JavaScript")`.