# Concat Method

**The `concat()` method returns a new array by merging two or more values/arrays.**

```jsx
let primeNumbers = [2, 3, 5, 7]
let evenNumbers = [2, 4, 6, 8]

// join two arrays 
let joinedArrays = primeNumbers.concat(evenNumbers);
console.log(joinedArrays);

/* Output:
[
  2, 3, 5, 7,
  2, 4, 6, 8 
]
*/
```

## **concat() Syntax**

The syntax of the `concat()` method is:

```jsx
arr.concat(value1, value2, ..., valueN)
```

Here, `arr` is an array.

## concat() Parameters

The `concat()` method takes in an arbitrary number of arrays and/or values as arguments.

## concat() Return Value

- Returns a newly created array after merging all arrays/values passed in the argument.

The `concat()` method first creates a new array with the elements of the object on which the method is called. It then sequentially adds arguments or the elements of arguments (for arrays).

## Example 1: Using concat() method

```jsx
var languages1 = ["JavaScript", "Python", "Java"];
var languages2 = ["C", "C++"];

// concatenating two arrays
var new_arr = languages1.concat(languages2);
console.log(new_arr); // [ 'JavaScript', 'Python', 'Java', 'C', 'C++' ]

// concatenating a value and array
var new_arr1 = languages2.concat("Lua", languages1);
console.log(new_arr1); // [ 'C', 'C++', 'Lua', 'JavaScript', 'Python', 'Java' ]
```

**Output**

```jsx
[ 'JavaScript', 'Python', 'Java', 'C', 'C++' ]
[ 'C', 'C++', 'Lua', 'JavaScript', 'Python', 'Java' ]
```

## Example 2: Concatenating nested arrays

The `concat()` method returns the shallow copy of the concatenated elements in the following way:

- It copies object references to the new array. (**For example**: passing a nested array) So if the referenced object is modified, the changes are visible in the returned new array.
- It copies the value of strings and numbers to the new array.

```jsx
var randomList = [1, 2, 3];
var randomNestedList = [
  [4, 5],
  [6, 7],
];

var combined = randomList.concat(randomNestedList);
console.log(combined); // [ 1, 2, 3, [ 4, 5 ], [ 6, 7 ] ]

// changing the value 1 to 0
randomList[0] = 0;
console.log(randomList); // [ 0, 2, 3 ]

// changes not reflected in concatenated array
console.log(combined); // [ 1, 2, 3, [ 4, 5 ], [ 6, 7 ] ]

// modifying nested list (adding 6 to first element)
randomNestedList[0].push(6);
console.log(randomNestedList); // [ [ 4, 5, 6 ], [ 6, 7 ] ]

// changes are reflected in concatenated array
// since it is a reference to the object
console.log(combined); // [ 1, 2, 3, [ 4, 5, 6 ], [ 6, 7 ] ]
```

**Output**

```jsx
[ 1, 2, 3, [ 4, 5 ], [ 6, 7 ] ]
[ 0, 2, 3 ]
[ 1, 2, 3, [ 4, 5 ], [ 6, 7 ] ]
[ [ 1, 2, 3 ], [ 6, 7 ] ]
[ 1, 2, 3, [ 4, 5, 6 ], [ 6, 7 ] ]
```

Here, the nested array's reference is copied to the concatenated array. So, when we modify any of the references, the changes are reflected everywhere.