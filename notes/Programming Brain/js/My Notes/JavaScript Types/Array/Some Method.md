# Some Method

**The `some()` method tests whether any of the array elements pass the given test function.**

```jsx
// a test function: returns an even number
function isEven(element) {
  return element % 2 === 0;
}

// defining an array
let numbers = [1, 3, 2, 5, 4];

// checks whether the numbers array contain at least one even number
console.log(numbers.some(isEven));

// Output: true 
```

## some() Syntax

The syntax of the `some()` method is:

```jsx
arr.some(callback(currentValue), thisArg)
```

## some() Parameters

The `some()` method can take **two** parameters:

- callback - The callback function to test for each array element. It takes in:
    - currentValue - The current element being passed from the array.
- thisArg (optional) - Value to use as this when executing . By default, it is `undefined`.
    
    callback
    

## some() Return Value

- Returns `true` if an array element passes the given test function (`callback` returns a truthy value).
- Otherwise, it returns `false`.

**Notes**: The `some()` method does not:

- change the original array.
- execute `callback` for array elements without values.

## Example 1: Using some() Method

```jsx
// a test function: returns age that is less that 18
function checkMinor(age) {
  return age < 18;
}

const ageArray = [34, 23, 20, 26, 12];

// checks whether ageArray contains any element that is less than 18
let check = ageArray.some(checkMinor);

console.log(check);
```

**Output**

```jsx
true
```

In the above example, we have used the `some()` method to find out whether any element of the ageArray array contains a value less than **18**.

At first, we created the callback function `checkMinor()` that returns age less than **18**.

We have then passed callback to the `some()` method as `ageArray.some(checkMinor)` that checks for elements less than **18** and returns `true`.

## Example 2: some() Method to Check Result of Students

```jsx
// array of scores obtained by student 
let scoreObtained = [45, 50, 39, 78, 65, 20];

// a test function: returns score less than 40
function studentIsPassed(score) {
  return score < 40;
}

// checks if score of at least one student is less than 40  
if(scoreObtained.some(studentIsPassed) == true) {
  console.log("At least one of the students failed.");
}

else
  console.log("All students are passed.");
```

**Output**

```jsx
At least one of the students failed.
```

In the above example, we have used the `some()` method to find out if any of the students have scored marks less than **40**.

We have passed callback in the method as `scoreObtained.some(studentIsPassed)` which returns

```jsx
true
```

because scoreObtained contains at least one element i.e. **20** which is less than **40**.

Since the test expression in the `if` statement is true, the program prints- `At least one of the students failed.`