# lndexOf()

The JavaScript string `indexOf()` method is used to search the position of a particular character or string in a sequence of given char values. This method is case-sensitive.

The index position of first character in a string is always starts with zero. If an element is not present in a string, it returns -1.

```jsx
const message = "JavaScript is not Java";

// returns index of 'v' in first occurrence of 'va'
const index = message.indexOf("va");

console.log('index: ' + index);  // index: 2
```

## Index OF Syntax

The syntax of the `indexOf()` method is:

```jsx
str.indexOf(searchValue, fromIndex)
```

## Index OF Parameters

The `indexOf()` method takes in:

- `searchValue` - The value to search for in the string. If no string is provided explicitly, "undefined" will be searched.
- `fromIndex` (optional) - The index to start the search at. By default it is 0. If fromIndex < 0, the search starts at index 0.

## Index OF Return Value

- Returns the first index of the value in the string if it is present at least once.
- Returns -1 if the value is not found in the string.