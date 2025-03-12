# Sort Method

**The `sort()` method sorts the items of an array in a specific order (ascending or descending).**

```jsx
let city = ["California", "Barcelona", "Paris", "Kathmandu"];

// sort the city array in ascending order
let sortedArray = city.sort();
console.log(sortedArray);

// Output: [ 'Barcelona', 'California', 'Kathmandu', 'Paris' ]
```

## sort() Syntax

The syntax of the `sort()` method is:

```jsx
arr.sort(compareFunction)
```

Here, arr is an array.

## sort() Parameters

The `sort()` method takes in:
• compareFunction (optional) - It is used to define a custom sort order.

## sort() Return Value

- Returns the array after sorting the elements of the array in place (meaning that it changes the original array and no copy is made).

## Example 1: Sorting the Elements of an Array

When `compareFunction` is not passed,

- All non-`undefined` array elements are first converted to [strings](https://www.programiz.com/javascript/string).
- These strings are then compared using their UTF-16 code point value.
- The sorting is done in ascending order.
- All `undefined` elements are sorted to the end of the array.

```jsx
// sorting an array of strings
var names = ["Adam", "Jeffrey", "Fabiano", "Danil", "Ben"];

// returns the sorted array
console.log(names.sort());

// modifies the array in place
console.log(names);

var priceList = [1000, 50, 2, 7, 14];
priceList.sort();

// Number is converted to string and sorted
console.log(priceList)
```

### Output

```
[ 'Adam', 'Ben', 'Danil', 'Fabiano', 'Jeffrey' ]
[ 'Adam', 'Ben', 'Danil', 'Fabiano', 'Jeffrey' ]
[ 1000, 14, 2, 50, 7 ]
```

Here, we can see that the names array is sorted in ascending order of the string. For example, Adam comes before Danil because "A" comes before "D".

Since all non-undefined elements are converted to strings before sorting them, the `Number` data types are sorted in that order.

Here, we can see that even though **1000** is greater than **50** numerically, it comes at the beginning of the sorted list. It is because **"1" < "5"**.

## Example 2: Sorting using Custom Function

When `compareFunction`is passed,

- All non-`undefined` array elements are sorted according to the return value of .
    
    compareFunction
    
- All undefined elements are sorted to the end of the array and  is not called for them.

Suppose we want to sort the above names array such that the longest name comes last, rather than sorting it alphabetically. We can do it in the following way:

```jsx
// custom sorting an array of strings
var names = ["Adam", "Jeffrey", "Fabiano", "Danil", "Ben"];

function len_compare(a, b){
    return a.length - b.length;
}

// sort according to string length
names.sort(len_compare);

console.log(names);
```

### Output

```
[ 'Ben', 'Adam', 'Danil', 'Jeffrey', 'Fabiano' ]
```

Here, the sorting is based on the logic `a.length - b.length`. It basically means that the item with shorter length will appear at the beginning of the `Array`.

Let's first understand how the optional `compareFunction` works.
Any `compareFunction` has the following syntax:

```jsx
function (a, b){
    // sorting logic
    // return a Number 
}
```

The `sort()` method compares all values of the array by passing two values at a time to the `compareFunction`. The two parameters a and b represent these two values respectively.

The `compareFunction` should return a `Number`. This returned value is used to sort the elements in the following way:

- If `returned value < 0`, `a` is sorted before `b` (`a` comes before `b`).
- If `returned value > 0`, `b` is sorted before `a` (`b` comes before `a`).
- If `returned value == 0`, `a` and `b` remain unchanged relative to each other.

In Example 2, we sort the array using:

```jsx
function len_compare(a, b){
    return a.length - b.length;
}
```

Here the break down:

- If `a.length - b.length < 0`, `a` comes before `b`. For example, `"Adam"` comes before `"Jeffrey`" as `4 - 7 < 0`.
- If `a.length - b.length > 0`, `b` comes before `a`. For example, `"Danil"` comes after `"Ben"` as `5 - 3 > 0`.
- If `a.length - b.length == 0`, their position is unchanged. For example, the relative position of `"Jeffrey"` and `"Fabiano"` is unchanged because `7 - 7 == 0`.

We can see that this results in the sorting of strings according to their length in ascending order.

## Example 3: Sorting Numbers Numerically

Since all non-undefined elements are converted to strings before sorting them, we cannot sort numbers using their numeric value by default.

Let's see how we can implement this using a custom function.

```jsx
// numeric sorting

// define array
var priceList = [1000, 50, 2, 7, 14];

// sort() using function expression
// ascending order
priceList.sort(function (a, b) {
  return a - b;
});

// Output: Ascending - 2,7,14,50,1000
console.log("Ascending - " + priceList);

// sort() using arrow function expression
// descending order
priceList.sort((a, b) => b - a);

// Output: Descending - 1000,50,14,7,2
console.log("Descending - " + priceList);
```

### Output

```jsx
Ascending - 2,7,14,50,1000
Descending - 1000,50,14,7,2
```

In this example, we sorted the array using:

```jsx
function (a, b) {
  return a - b;
}
```

Here,

- If `a - b < 0`, `a` comes before `b`. For example, `2` comes before `7` as `2 - 7 < 0`.
- If `a - b > 0`, `b` comes before `a`. For example, `1000` comes after `50` as `1000 - 50 > 0`.

We can see that this results in the sorting of the numbers according to their ascending numeric value.

Similarly, we can use `b - a` to sort them in descending order. Note that we can also use the arrow function expression defined in ES2015.

We can also reverse (descending order) the sorted array using the built-in array `reverse()` method.