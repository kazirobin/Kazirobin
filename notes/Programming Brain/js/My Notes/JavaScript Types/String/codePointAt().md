# codePointAt()

The `codePointAt()` method of Character class is used to return the code point at the given index of char array. If at a particular index, the char value in the char array is in the high surrogate range, the following index is less than the index of char array and if the char value at a given index is in the low surrogate range then the codepoint corresponding to this pair is returned.

```jsx
let message = "Happy Birthday";

// unicode point of character at index 1
let codePoint1 = message.codePointAt(1);

console.log("Unicode Code Point of 'a' is " + codePoint1);

// Output
// Unicode Code Point of 'a' is 97
```

## Code Point At Syntax

The `codePointAt()` method takes a single parameter. and The syntax of the `codePointAt()` method is:

```jsx
str.codePointAt(index)
```

## Code Point At Parameters

The `codePointAt()` method takes a single parameter:

- `pos` - index value of an element in `str`

## Code Point At Return Value

The `codePointAt()` method returns:

- a number representing the unicode point value of the character at the given `pos`
- `undefined` if no element is found at `pos`