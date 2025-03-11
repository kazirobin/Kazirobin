# Every Method

**The `every()` method checks if all the array elements pass the given test function.**

```jsx
// function that checks whether
// the age is 18 or above
function checkAdult(age) {
    return age >= 18;
}

const ageArray = [34, 23, 20, 26, 12];

//checks if all the array elements
// pass the checkAdult() function
let check = ageArray.every(checkAdult);

// Output: false
```

## every() Syntax

The syntax of the `every()` method is:

```jsx
arr.every(callback(currentValue), thisArg)
```

## every() Parameters

The `every()` method takes in:

- callback() - the function to test for each array element. It takes in:
    - `currentValue` - the current element being passed from the array.
- `thisArg` (optional) - value to use as this when executing `callback()`. By default, it is `undefined`.

## every() Return Value

The `every()` method returns:

- **true** - if all the array elements pass the given test function (`callback` returns a truthy value).
- **false** - if any array element fails the given test function.

**Notes**:

- `every()` does not change the original array.
- `every()` does not execute the `callback()` function for an empty array. In case we do pass an empty array, it always returns true.

## Example 1: Check if Array Elements Are Even

```jsx
// function that checks whether all
// the array elements are even or not
function checkEven(num) {
    return num%2 === 0;
}

// create an array of numbers
const numbers = [2, 4, 6, 7, 8];

// use the every() method along with
// checkEven() on the numbers array
let check = numbers.every(checkEven); 

console.log(check)

// Output: false
```

In the above example, we have created the `checkEven()` function that checks whether a given number is even or not.

We then call the `every()` method on the `numbers` array. Since there is an odd number (**7)** in the array, we get `false` as an output.

## Example 2: JavaScript every() With Arrow Function

```jsx
let numbers = [ 1 , 2 , 3 , 4 , 5];

// use arrow function with every()
let result = numbers.every(element => element < 6);
console.log(result); 

// Output: true
```

In the above example, we have created the `numbers` array. Then, we call the `every()` method on that array.

Notice the arrow function `element=> element < 6` inside the `every()` method. This function checks whether a given array element is less than **6** or not.

Since, all the elements in the `numbers` array are less than **6**, we get `true` as an output.