# charAt()

The JavaScript string charAt() method is used to find out a char value present at the specified index in a string.

The index number starts from 0 and goes to n-1, where n is the length of the string. The index value can't be a negative, greater than or equal to the length of the string.

```jsx
// string declaration
const string1 = "Hello World!";

// finding character at index 8
let index8 = string1.charAt(8);

console.log("Character at index 8 is " + index8);
```

## CharAt Syntax

The syntax of the `charAt()` method is:

```jsx
str.charAt(index)
```

## CharAt Parameters

The `charAt()` method takes in:

- `index` - An integer between 0 and str.length - 1. If index cannot be converted to integer or is not provided, the default value 0 is used.

## CharAt Return Value

- Returns a string representing the character at the specified `index`