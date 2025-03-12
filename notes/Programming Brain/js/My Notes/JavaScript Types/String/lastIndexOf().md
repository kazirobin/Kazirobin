# lastIndexOf()

The JavaScript string `lastIndexOf()` method is used to search the position of a particular character or string in a sequence of given char values. It behaves similar to `indexOf()` method with a difference that it start searching an element from the last position of the string.

The `lastIndexOf()` method is case-sensitive. The index position of first character in a string is always starts with zero. If an element is not present in a string, it returns -1.

```jsx
// defining a string
var str = "Programming";

var substr = "g";

// find last occurrence of "g" in str
var result = str.lastIndexOf(substr);

console.log(result);

// Output: 10
```

## Last Index OF Syntax

The syntax of the `lastIndexOf()` method is:

```jsx
str.lastIndexOf(searchValue, fromIndex)
```

## Last Index OF Parameters

The `lastIndexOf()` method takes in:

- `substr`The value to search for in the given string.
- `fromIndex` (optional) - The index to start searching the string backwards. By default it is +Infinity.

## Last Index OF Return Value

The `lastIndexOf()` method returns:

- the last index of the value in the string if it is present at least once.
- `fromIndex` if no string is provided explicitly.