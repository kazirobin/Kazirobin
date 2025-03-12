# Find Method

**The `find()` method returns the value of the first array element that satisfies the provided test function.**

```jsx
let numbers = [1, 3, 4, 9, 8];

// function to check even number
function isEven(element) {
  return element % 2 == 0;
}

// get the first even number
let evenNumber = numbers.find(isEven);
console.log(evenNumber);

// Output: 4
```

## find() Syntax

The syntax of the `find()` method is:

```jsx
arr.find(callback(element, index, arr),thisArg)
```

Here, `arr` is an array.

## find() Parameters

The `find()` method takes in:

- callback - Function to execute on each element of the array. It takes in:
    - element - The current element of array.
    - index (optional) - The index of the current element.
    - arr (optional) - The array of the current element.
- thisArg (optional) - Object to use as `this` inside .
    
    callback
    

## find() Return Value

- Returns the **value** of the **first element** in the array that satisfies the given function.
- Returns  if none of the elements satisfy the function.
    
    undefined
    

## Example 1: Using find() method

```jsx
function isEven(element) {
  return element % 2 == 0;
}

let randomArray = [1, 45, 8, 98, 7];

let firstEven = randomArray.find(isEven);
console.log(firstEven); // 8

// using arrow operator
let firstOdd = randomArray.find((element) => element % 2 == 1);
console.log(firstOdd); // 1
```

**Output**

```jsx
8
1
```

## Example 2: find() with Object elements

```jsx
const team = [
  { name: "Bill", age: 10 },
  { name: "Linus", age: 15 },
  { name: "Alan", age: 20 },
  { name: "Steve", age: 34 },
];

function isAdult(member) {
  return member.age >= 18;
}

console.log(team.find(isAdult)); // { name: 'Alan', age: 20 }

// using arrow function and deconstructing
let adultMember = team.find(({ age }) => age >= 18);

console.log(adultMember); // { name: 'Alan', age: 20 }
```

**Output**

```jsx
{ name: 'Alan', age: 20 }
{ name: 'Alan', age: 20 }
```