# Space Complexity

Space complexity is a measure of the amount of working storage an algorithm needs. It's expressed in terms of the size of the input, typically using Big O notation. It helps in analyzing how an algorithm scales with larger inputs.

## Components of Space Complexity

- **Fixed Space**: This is the space required for variables and constants. For example, if you use a few variables to store integers or strings, this will be constant space.
- **Dynamic Space**: This refers to the space required for data structures whose size may change, such as arrays, objects, or any data structure that grows with input.
- **Auxiliary Space**: This is the extra space or temporary space used by an algorithm, not counting the input size.

## Analyzing Space Complexity

When analyzing space complexity, you usually consider the following:

- **Primitive Variables**: Constants and primitive data types (like numbers, booleans) require a fixed amount of space.
- **Data Structures**: The space complexity depends on how much data you are storing. For instance:
    - An array of `n` elements has a space complexity of `O(n)`
    - A nested data structure (like an object within an array) may have a more complex space requirement, depending on how it's structured.
- **Recursion**: Recursive algorithms can consume extra space due to the call stack. For instance, a simple recursive function can lead to a space complexity of `O(n)` in the case of a linear recursion depth.

## Constant Space Complexity `O(1)`

This means that the algorithm uses a fixed amount of space regardless of the input size.

### Example: Checking Even or Odd

```jsx
function isEven(num) {
    return num % 2 === 0; // Only uses a constant amount of space
}
```

**Space Complexity**: `O(1)`

**Explanation**: The function uses a single variable (`num`), so the memory required does not change with input size.

## Linear Space Complexity `O(n)`

This occurs when the space used grows linearly with the size of the input.

### Example: Duplicating an Array

```jsx
function duplicateArray(arr) {
    let newArr = []; // O(1) for the new array reference
    for (let i = 0; i < arr.length; i++) {
        newArr[i] = arr[i]; // O(n) for copying n elements
    }
    return newArr;
}

// Usage
const originalArray = [1, 2, 3, 4];
const copiedArray = duplicateArray(originalArray);
```

**Space Complexity**: `O(n)`

**Explanation**: The new array `newArr` is created, which takes up space proportional to the size of `arr`.

## Quadratic Space Complexity `O(n2)`

This happens when the algorithm uses space proportional to the square of the input size.

### Example: Creating an `n x n` Matrix

```jsx
function createMatrix(n) {
    let matrix = []; // O(1)
    for (let i = 0; i < n; i++) {
        matrix[i] = []; // Create a new row
        for (let j = 0; j < n; j++) {
            matrix[i][j] = 0; // Initialize elements
        }
    }
    return matrix;
}

// Usage
const n = 3;
const matrix = createMatrix(n);
```

**Space Complexity**: `O(n2)`

**Explanation**: The matrix has `n` rows and `n` columns, leading to `n^2` elements in total.

## Recursive Space Complexity `O(n)`

Recursive functions can use additional space due to the call stack.

### Example: Factorial Calculation

```jsx
function factorial(n) {
    if (n <= 1) return 1; // Base case
    return n * factorial(n - 1); // Recursive call
}

// Usage
const result = factorial(5);
```

**Space Complexity:** `O(n)`

**Explanation**: Each recursive call adds a new layer to the call stack. For `factorial(5)`, there are 5 calls in the stack.

## Space Complexity in Data Structures

Different data structures can have varying space complexities based on how they store data.

### Example: Using an Object

```jsx
function countCharacters(str) {
    let charCount = {}; // O(1) for the object reference
    for (let char of str) {
        if (charCount[char]) {
            charCount[char]++; // Increment count
        } else {
            charCount[char] = 1; // Initialize count
        }
    }
    return charCount;
}

// Usage
const result = countCharacters("hello");
```

**Space Complexity:** `O(k)`, where `k` is the number of unique characters in the string.

**Explanation**: The object `charCount` grows based on the unique characters in `str`.

## Summary of Space Complexity

| Space Complexity | Big O Notation |
| --- | --- |
| Constant | O(1) |
| Logarithmic | O(logn) |
| Linear | O(n) |
| Quadratic | O(n^2) |
| Cubic | O(n^2) |
| Exponential | O(2^n) |
| Factorial | O(n!) |