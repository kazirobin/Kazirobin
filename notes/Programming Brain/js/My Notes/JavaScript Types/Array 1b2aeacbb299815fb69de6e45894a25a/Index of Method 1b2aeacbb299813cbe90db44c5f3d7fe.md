# Index of Method

**The `indexOf()` method returns the first index of occurrence of an array element, or -1 if it is not found.**

```jsx
let languages = ["Java", "JavaScript", "Python", "JavaScript"];

// get the index of the first occurrence of "JavaScript"
let index = languages.indexOf("JavaScript");
console.log(index);

// Output: 1
```

## indexOf() Syntax

The syntax of the `indexOf()` method is:

```jsx
arr.indexOf(searchElement, fromIndex)
```

Here, arr is an array.

## indexOf() Parameters

The `indexOf()` method takes in:

- searchElement - The element to locate in the array.
- fromIndex (optional) - The index to start the search at. By default, it is **0**.

## indexOf() Return Value

- Returns the first index of the element in the array if it is present at least once.
- Returns **1** if the element is not found in the array.

**Note:** `indexOf()` compares `searchElement` to elements of the Array using **strict equality** (similar to triple-equals operator or `===`).

## Example 1: Using indexOf() method

```jsx
var priceList = [10, 8, 2, 31, 10, 1, 65];

// indexOf() returns the first occurance
var index1 = priceList.indexOf(31);
console.log(index1); // 3

var index2 = priceList.indexOf(10);
console.log(index2); // 0

// second argument specifies the search's start index
var index3 = priceList.indexOf(10, 1);
console.log(index3); // 4

// indexOf returns -1 if not found
var index4 = priceList.indexOf(69.5);
console.log(index4); // -1
```

**Output**

```jsx
3
0
4
-1
```

**Note:**

- If **fromIndex >= array.length**, array is not searched and **1** is returned.
- If **fromIndex < 0**, the index is calculated backward. For example, **1** denotes the last element's index and so on.

## Example 2: Finding All the Occurrences of an Element

```jsx
function findAllIndex(array, element) {
  indices = [];
  var currentIndex = array.indexOf(element);
  while (currentIndex != -1) {
    indices.push(currentIndex);
    currentIndex = array.indexOf(element, currentIndex + 1);
  }
  return indices;
}

var priceList = [10, 8, 2, 31, 10, 1, 65, 10];

var occurance1 = findAllIndex(priceList, 10);
console.log(occurance1); // [ 0, 4, 7 ]

var occurance2 = findAllIndex(priceList, 8);
console.log(occurance2); // [ 1 ]

var occurance3 = findAllIndex(priceList, 9);
console.log(occurance3); // []
```

**Output**

```jsx
[ 0, 4, 7 ]
[ 1 ]
[]
```

## Example 3: Finding If Element exists else Adding the Element

```jsx
function checkOrAdd(array, element) {
  if (array.indexOf(element) === -1) {
    array.push(element);
    console.log("Element not Found! Updated the array.");
  } else {
    console.log(element + " is already in the array.");
  }
}

var parts = ["Monitor", "Keyboard", "Mouse", "Speaker"];

checkOrAdd(parts, "CPU"); // Element not Found! Updated the array.
console.log(parts); // [ 'Monitor', 'Keyboard', 'Mouse', 'Speaker', 'CPU' ]

checkOrAdd(parts, "Mouse"); // Mouse is already in the array.
```

**Output**

```jsx
Element not Found! Updated the array.
[ 'Monitor', 'Keyboard', 'Mouse', 'Speaker', 'CPU' ]
Mouse is already in the array.
```