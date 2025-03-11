# concat()

The JavaScript string concat() method combines two or more strings and returns a new string. This method doesn't make any change in the original string.

```jsx
let emptyString = "I Love";

// joint arguments string
let joinedString = emptyString.concat(" ", "JavaScript.");
console.log(joinedString);

// Output: I Love JavaScript.
```

## Concat Syntax

The syntax of the `concat()` method is below:

```jsx
str.concat(str1, str2, str3)
```

## Concat Parameters

The `concat()` method takes in an arbitrary number of strings to concatenate to `str`.

## Concat Return Value

- Returns a new string containing the combined text of the strings provided.