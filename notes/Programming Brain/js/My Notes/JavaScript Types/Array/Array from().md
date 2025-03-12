# Array.from()

The `from()` method creates a new array from any array-like or iterable object.

```jsx
// creating a new array from string
let newArray = Array.from("abc");

console.log(newArray);

// Output:
// [ 'a', 'b', 'c' ]
```

## from() Syntax

The syntax of the `from()` method is:

```jsx
Array.from(arraylike, mapFunc, thisArg)
```

The `from()` method, being a static method, is called using the `Array` class name.

## from() Parameters

The `from()` method can take **three** parameters:

- `arraylike` - Array-like or iterable object to convert to an array.
- `mapFunc` (optional) - Map function that is called on each element.
- `thisArg` (optional) - Value to use as this when executing mapFunc.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note**: `Array.from(obj, mapFunc, thisArg)` is equivalent to `Array.from(obj).map(mapFunc, thisArg)`.

</aside>

## from() Return Value

Returns a new `Array` instance.

<aside>
<img src="https://www.notion.so/icons/new-alert_yellow.svg" alt="https://www.notion.so/icons/new-alert_yellow.svg" width="40px" /> **Note**: This method can create an array from:

- array-like objects - The objects that have length property and have indexed elements like `String`.
- Iterable objects like Map or Set.
</aside>

## Example 1: from() Method with Array-like Objects

```jsx
// creating an array from a string 
let array1= Array.from("JavaScript");

console.log(array1);

// Output:
// ['J', 'a', 'v', 'a', 'S', 'c', 'r', 'i', 'p', 't']
```

In the above example, we have used the `from()` method to create a new array from the `'JavaScript'` string.

We have called the method using `Array` class as `Array.from("JavaScript")`. The method returns a new array `['J', 'a', 'v', 'a', 'S', 'c', 'r', 'i', 'p', 't']` and assigns it to array1.

## Example 2: from() Method with Mapping Function

```jsx
// function that returns a new array
function createArray(arraylike, mapFunc) {
  return Array.from(arraylike, mapFunc);
}

// using arrow function for mapFunc
let result = createArray([2, 4, 6], (element) => element + 2);

console.log(result);

// Output:
// [ 4, 6, 8 ]
```

In the above example, we have passed a mapping function in the `from()` method that increases every element of the array being created by **2**.

## Example 2: from() Method with a Set

```jsx
// defining a Set
let set = new Set(["JavaScript", "Python", "Go", "Python"]);

// creating an array from the given  set
let result = Array.from(set);

console.log(result);

// Output:
// [ 'JavaScript', 'Python', 'Go' ]
```

Here, we have created a new array using the `from()` method with an iteratable object- `Set`.