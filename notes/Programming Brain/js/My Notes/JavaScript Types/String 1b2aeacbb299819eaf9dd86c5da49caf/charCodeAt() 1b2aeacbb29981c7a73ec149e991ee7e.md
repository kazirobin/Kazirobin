# charCodeAt()

The JavaScript string `charCodeAt()` method is used to find out the Unicode value of a character at the specific index in a string.

The index number starts from 0 and goes to n-1, where n is the length of the string. It returns `NaN` if the given index number is either a negative number or it is greater than or equal to the length of the string.

```jsx
// string definition
const greeting = "Good morning!";

// UTF-16 code unit of character at index 5
let result = greeting .charCodeAt(5);

console.log(result);

// Output: 109
```

## Char Code At Syntax

The syntax of the `charCodeAt()` method is:

```jsx
str.charCodeAt(index)
```

## Char Code At Parameters

The `charCodeAt()` method takes a single parameter:

- `index` - An integer between 0 and (str.length - 1)

## Char Code At Return Value

- Returns a number representing the UTF-16 code unit value of the character at the given index.