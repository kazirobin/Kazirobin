# For Each Method

**The `forEach()` method executes a provided function for each array element.**

```jsx
let numbers = [1, 3, 4, 9, 8];

// function to compute square of each number
function computeSquare(element) {
  console.log(element * element);
}

// compute square root of each element
numbers.forEach(computeSquare);

/* Output:
1
9 
16
81
64
*/
```

## forEach() Syntax

The syntax of the `forEach()` method is:

```jsx
arr.forEach(callback(currentValue, index, arr), thisArg)
```

Here, `arr` is an array.

## forEach() Parameters

The `forEach()` method takes in:

- callback - The callback function to execute on every array element. It takes in:
    - currentValue - The current element being passed from the array.
    - index (optional) - The index of the current element.
    - arr (optional) - The array of the current element.
- thisArg (optional) - Value to use as this when executing . By default, it is `undefined`.
    
    callback
    

## forEach() Return Value

Returns `undefined`.

**Notes:**

- `forEach()` does not change the original array.
- `forEach()` executes `callback` once for each array element in order.
- `forEach()` does not execute `callback` for array elements without values.

## Example 1: Printing Contents of Array

```jsx
function printElements(element, index) {
    console.log('Array Element ' + index + ': ' + element);
}

const prices = [1800, 2000, 3000, , 5000, 500, 8000];

// forEach does not execute for elements without values
// in this case, it skips the third element as it is empty
prices.forEach(printElements);
```

**Output**

```jsx
Array Element 0: 1800
Array Element 1: 2000
Array Element 2: 3000
Array Element 4: 5000
Array Element 5: 500
Array Element 6: 8000
```

## Example 2: Using thisArg

```jsx
function Counter() {
    this.count = 0;
    this.sum = 0;
    this.product = 1;
}

Counter.prototype.execute = function (array) {
    array.forEach((entry) => {
        this.sum += entry;
        ++this.count;
        this.product *= entry;
    }, this)
}

const obj = new Counter();
obj.execute([4, 1, , 45, 8]);

console.log(obj.count); // 4

console.log(obj.sum); // 58

console.log(obj.product); // 1440
```

**Output**

```jsx
4
58
1440
```

Here, we can again see that `forEach` skips the empty element. `thisArg` is passed as `this` inside the definition of the `execute` method of the Counter object.