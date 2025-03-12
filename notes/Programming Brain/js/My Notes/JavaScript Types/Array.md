# Array

An array in JavaScript is a type of global object that is used to store data. An array is an ordered data collection (either primitive or object depending upon the language). Arrays are used to store multiple values under a single variable name. A regular variable, on the other hand, can store only one value.

Each item in an array has a number attached to it, called a numeric index, that allows you to access it. In JavaScript, arrays start at index zero and can be manipulated with various methods.

Here, `words` is an array. The array is storing 3 values.

```jsx
const words = ['hello', 'world', 'welcome'];
```

## Create an Array

You can create an array using two ways:

### 1. Using an array literal

The easiest way to create an array is by using an array literal `[ ]`. For example,

```jsx
const array = ["eat", "sleep"];
```

### 2. Using the new keyword

You can also create an array using JavaScript's `new` keyword.

```jsx
const array = new Array("eat", "sleep");
```

Here are more examples of arrays:

```jsx
// empty array
const myList = [ ];

// array of numbers
const numberArray = [ 2, 4, 6, 8];

// array of strings
const stringArray = [ 'eat', 'work', 'sleep'];

// array with mixed data types
const newData = ['work', 'exercise', 1, true];
```

## Access Elements of an Array

You can access elements of an array using indices **(0, 1, 2 …)**. For example

```jsx
const myArray = ['h', 'e', 'l', 'l', 'o'];

// first element
console.log(myArray[0]);  // "h"

// second element
console.log(myArray[1]); // "e"
```

Array's index starts with 0, not 1.

![array_index.png](Array%201b2aeacbb299815fb69de6e45894a25a/array_index.png)

## Add an Element to an Array

You can use the built-in method `push( )` and `unshift( )` to add elements to an array.

The `push( )` method adds an element at the end of the array. For example,

```jsx
let array = ['eat', 'sleep'];

// add an element at the end
array .push('exercise');

console.log(array); //  ['eat', 'sleep', 'exercise']
```

The `unshift( )` method adds an element at the beginning of the array. For example,

```jsx
let array = ['eat', 'sleep'];

//add an element at the start
array.unshift('work'); 

console.log(array); // ['work', 'eat', 'sleep']
```

## Change the Elements of an Array

You can also add elements or change the elements by accessing the index value.

```jsx
let array = [ 'eat', 'sleep'];

// this will add the new element 'exercise' at the 2 index
array[2] = 'exercise';

console.log(array); // ['eat', 'sleep', 'exercise']
```

Suppose, an array has two elements. If you try to add an element at index 3 (fourth element), the third element will be undefined. For example,

```jsx
let array = [ 'eat', 'sleep'];

// this will add the new element 'exercise' at the 3 index
array[3] = 'exercise';

console.log(array); // ["eat", "sleep", undefined, "exercise"]
```

Basically, if you try to add elements to high indices, the indices in between will have undefined values.

## Remove an Element from an Array

You can use the `pop( )` method to remove the last element from an array. The `pop( )` method also returns the returned value. For example,

```jsx
let array = ['work', 'eat', 'sleep', 'exercise'];

// remove the last element
array.pop();
console.log(array); // ['work', 'eat', 'sleep']

// remove the last element from ['work', 'eat', 'sleep']
const removedElement = array.pop();

//get removed element
console.log(removedElement); // 'sleep'
console.log(array);  // ['work', 'eat']
```

If you need to remove the first element, you can use the `shift( )` method. The `shift( )` method removes the first element and also returns the removed element. For example,

```jsx
let array = ['work', 'eat', 'sleep'];

// remove the first element
array.shift();

console.log(array); // ['eat', 'sleep']
```

## Array length

You can find the length of an element (the number of elements in an array) using the `length` property. For example,

```jsx
const array = [ 'eat', 'sleep'];

// this gives the total number of elements in an array
console.log(array.length); // 2
```

## Popular Array Methods

In JavaScript, there are various array methods available that make it easier to perform useful calculations.

Some of the commonly used JavaScript array methods are:

| Method | Description |
| --- | --- |
| concat( ) | joins two or more arrays and returns a result |
| indexOf( ) | searches an element of an array and returns its position |
| find( ) | returns the first value of an array element that passes a test |
| findIndex( ) | returns the first index of an array element that passes a test |
| forEach( ) | calls a function for each element |
| map() | creates a new array from calling a function for every array element. |
| filter() | creates a new array filled with elements that pass a test provided by a function. |
| includes( ) | checks if an array contains a specified element |
| push( ) | aads a new element to the end of an array and returns the new length of an array |
| unshift( ) | adds a new element to the beginning of an array and returns the new length of an array |
| pop( ) | removes the last element of an array and returns the removed element |
| shift( ) | removes the first element of an array and returns the removed element |
| sort( ) | sorts the elements alphabetically in strings and in ascending order |
| reverse() | reverses the order of the elements in an array. |
| slice( ) | selects the part of an array and returns the new array |
| splice( ) | removes or replaces existing elements and/or adds new elements |
| join() | returns an array as a string |
| reduce() | executes a reducer function for array element. |
| keys() | returns an Array Iterator object with the keys of an array. |

## Array Methods in Details

In JavaScript, there are various array methods available that make it easier to perform useful calculations.

[Concat Method](Array%201b2aeacbb299815fb69de6e45894a25a/Concat%20Method%201b2aeacbb2998149ae6ff28ef2edddf9.md)

[Find Method](Array%201b2aeacbb299815fb69de6e45894a25a/Find%20Method%201b2aeacbb29981a5b96ded6309dc4ade.md)

[Find Index Method](Array%201b2aeacbb299815fb69de6e45894a25a/Find%20Index%20Method%201b2aeacbb2998163accbe0551978227b.md)

[For Each Method](Array%201b2aeacbb299815fb69de6e45894a25a/For%20Each%20Method%201b2aeacbb2998193bedee929769f4e0f.md)

[Index of Method](Array%201b2aeacbb299815fb69de6e45894a25a/Index%20of%20Method%201b2aeacbb299813cbe90db44c5f3d7fe.md)

[**Array.from()**](Array%201b2aeacbb299815fb69de6e45894a25a/Array%20from()%201b2aeacbb29981f4aa4fea6b03c0b4fb.md)

[Sort Method](Array%201b2aeacbb299815fb69de6e45894a25a/Sort%20Method%201b2aeacbb299810fa0bbef35f4c52c68.md)

[Some Method](Array%201b2aeacbb299815fb69de6e45894a25a/Some%20Method%201b2aeacbb29981b586c9d90c9f3def52.md)

[Every Method](Array%201b2aeacbb299815fb69de6e45894a25a/Every%20Method%201b2aeacbb29981a1a7b3cc58322f775b.md)