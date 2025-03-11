# Find Index Method

The `findIndex()` method returns the index of the first array element that satisfies the provided test function or else returns -1.

```jsx
// function that returns odd number
function isOdd(element) {
  return element % 2 !== 0;
}

// defining an array of integers
let numbers = [2, 8, 1, 3, 4];

// returns the index of the first odd number in the array
let firstOdd = numbers.findIndex(isOdd);

console.log(firstOdd);

// Output: 2
```

## findIndex() Syntax

The syntax of the `findIndex()` method is:

```jsx
arr.findIndex(callback(element, index, arr),thisArg)
```

Here, `arr` is an array.

## findIndex() Parameters

The `findIndex()` method can take **two** parameters:

- callback - Function to execute on each element of the array. It takes in:
    - element - The current element of array.
    - index (optional) - The index of the current element.
    - arr (optional) - The array of the current element.
- thisArg (optional) - Object to use as `this` inside .
    
    callback
    

## findIndex() Return Value

- Returns the **index** of the **first element** in the array that satisfies the given function.
- Returns **1** if none of the elements satisfy the function.

## Example 1: Using findIndex() method

```jsx
// function that returns even number
function isEven(element) {
  return element % 2 == 0;
}

// defining an array of integers
let numbers = [1, 45, 8, 98, 7];

// returns the index of the first even number in the array
let firstEven = numbers.findIndex(isEven);

console.log(firstEven); // 2
```

**Output**

```jsx
2
```

In the above example, we have used the `findIndex()` method to find the index of the first even number in the numbers array.

`isEven()` is a function that returns an even number. We have passed `isEven()` as a callback in the `findIndex()` method as- `numbers.findIndex(isEven)`.

The method returns **2** which is the index of the first even number in numbers i.e. **8**.

## Example 2: findIndex() with Arrow Function

```jsx
// defining an array
let days = ["Sunday", "Wednesday", "Tuesday", "Friday"];

// returns the first index of 'Wednesday' in the array
let index = days.findIndex((day) => day === "Wednesday");

console.log(index); // 1
```

**Output**

```jsx
1
```

Here we have passed an arrow function as a callback in the `findIndex()` method. The method returns the first index of `'Wednesday'`.

## Example 3: findIndex() with Object Elements

```jsx
// defining an object 
const team = [
  { name: "Bill", age: 10 },
  { name: "Linus", age: 15 },
  { name: "Alan", age: 20 },
  { name: "Steve", age: 34 },
];

// function that returns age greater than or equal to 18
function isAdult(member) {
  return member.age >= 18;
}

// returns the index of the first element which is 
// greater than or equal to 18  
console.log(team.findIndex(isAdult)); // 2
```

**Output**

```jsx
2
```