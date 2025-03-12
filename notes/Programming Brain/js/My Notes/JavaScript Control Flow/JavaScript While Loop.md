# JavaScript While Loop

The **`while`** statement creates a loop that executes a specified statement as long as the test condition evaluates to true. The condition is evaluated before executing the statement.

The syntax of the `while` loop is:

```jsx
while (condition) {
    // body of loop
}
```

Here,

1. The `while` loop first evaluates the condition inside `( )`.
2. If the condition evaluates to `true`, the code inside `{ }` is executed.
3. Then, the condition is evaluated again.
4. This process continues as long as the condition evaluates to `true`.
5. If the condition evaluates to `false`, the loop stops.

## Flowchart of while Loop

![Screenshot_1.jpg](JavaScript%20While%20Loop%201b2aeacbb2998182bc9ec1356ed4a934/Screenshot_1.jpg)

## Example 1: Display Numbers From 1 to 3

```jsx
// initialize variable i
let i = 1;

// loop runs until i is less than 4
while (i < 4) {
    console.log(i);
    i += 1;
}

// output: 1, 2, 3
```

Here is how the above program works in each iteration of the loop:

| Variable | Condition: i < 4 | Action |
| --- | --- | --- |
| i = 1 | true | **1** is printed. i is increased to **2**. |
| i = 2 | true | **2** is printed. i is increased to **3**. |
| i = 3 | true | **3** is printed. i is increased to **4**. |
| i = 4 | false | The loop is terminated. |

## Example 2: Sum of Only Positive Numbers

```jsx
let num = 0, sum = 0;

// loop as long as num is 0 or positive
while (num >= 0) {

    // add all positive numbers
    sum += num;

    // take input from the user
    num = parseInt(prompt("Enter a number: "));
}

// last, display sum
console.log(`The sum is ${sum}`);
```

### Output

```jsx
Enter a number: 2
Enter a number: 4
Enter a number: -3
The sum is 6
```

The above program prompts the user to enter a number.

Since JavaScript `prompt()` only takes inputs as [string](https://www.programiz.com/javascript/string), `parseInt()` converts the input to a number.

As long as we enter positive numbers, the `while` loop adds them up and prompts us to enter more numbers.

So when we enter a negative number, the loop terminates.
Finally, we display the total sum of positive numbers.

**Note:** When we add two or more numeric strings, JavaScript treats them as strings. For example, `"2" + "3" = "23"`. So, we should always convert numeric strings to numbers to avoid unexpected behaviors.

## JavaScript do...while Loop

The `do...while` loop executes a block of code once, then repeatedly executes it as long as the specified condition is `true`.

The syntax of the `do...while` loop is:

```jsx

do {
    // body of loop
} while(condition);
```

Here,

1. The `do…while` loop executes the code inside `{ }`.
2. Then, it evaluates the condition inside `( )`.
3. If the condition evaluates to `true`, the code inside `{ }` is executed again.
4. This process continues as long as the condition evaluates to `true`.
5. If the condition evaluates to `false`, the loop terminates.

## Flowchart of do...while Loop

![Screenshot_2.jpg](JavaScript%20While%20Loop%201b2aeacbb2998182bc9ec1356ed4a934/Screenshot_2.jpg)

## Example 3: Display Numbers from 3 to 1

```jsx
let i = 3;

// do...while loop
do {
    console.log(i);
    i--;
} while (i > 0);

// output: 3, 2, 1
```

Here, the initial value of i is **3**. Then, we used a `do...while` loop to iterate over the values of i. Here is how the loop works in each iteration:

| Action | Variable | Condition: i > 0 |
| --- | --- | --- |
| **3** is printed. i is decreased to **2**. | i = 2 | true |
| **2** is printed. i is decreased to **1**. | i = 1 | true |
| **1** is printed. i is decreased to **0**. | i = 0 | false |

The loop is terminated.

### **What is the difference between while and do...while loops.**

The difference between `while` and `do...while` is that the `do...while` loop executes its body at least once. For example,

```jsx
let i = 0;

// false condition
// body executes once
do {
    console.log(i);
} while (i > 1);

// Output: 0
```

On the other hand, the `while` loop doesn't execute its body if the loop condition is `false`. For example,

```jsx
let i = 0;

// false condition
// body not executed
while (i > 1) {
    console.log(i);
};
```

## Example 4: Sum of Positive Numbers

```jsx
let sum = 0, num = 0;

do {

    // add all positive numbers
    sum += num;

    // take input from the user
    num = parseInt(prompt("Enter a number: "));

    // loop terminates if num is negative
} while (num >= 0);

// last, display sum
console.log(`The sum is ${sum}`);
```

### Output

```jsx
Enter a number: 2
Enter a number: 4
Enter a number: -3
The sum is 6
```

In the above program, the `do...while` loop prompts the user to enter a number.
As long as we enter positive numbers, the loop adds them up and prompts us to enter more numbers.

If we enter a negative number, the loop terminates without adding the negative number.

### **What is an infinite while loop in JavaScript?**

An infinite `while` loop is a condition where the loop runs infinitely, as its condition is always `true`. For example,

```jsx
let i = 1;

// always true condition
while(i < 5) {
    console.log(i);
}
```

Also, here is an example of an infinite `do...while` loop,

```jsx
let i = 5;

// always true condition
do {
    console.log(i);
} while (i > 1);
```

In the above program, the condition `1` `> 1` is always `true`, which causes the loop body to run forever.

**Note:** Infinite loops can cause your program to hang. So, avoid creating them unintentionally.

### **What is the difference between for and while loops?**

We use a `for` loop when we need to perform a fixed number of iterations. For example,

```jsx
// display hi 3 times

for (let i = 1; i <= 3; i++) {
    console.log("hi");
}

console.log("bye");
```

Mean while, we use a `while` loop when the termination condition can vary. For example,

```jsx
// display hi as long as user wants
let isDisplay = true;
let userChoice = "";

while (isDisplay) {
    console.log("hi");

    userChoice = prompt("print hi again? y for yes: ");
    if (userChoice != "y")
        isDisplay = false;
}

console.log("bye");
```

### Output

```jsx
hi
print hi again? y for yes: y
hi
print hi again? y for yes: y
hi
print hi again? y for yes: n
bye
```

In the above program, we let the user print `hi` as much as they desire.
Since we don't know the user's decision, we use a `while` loop instead of a `for` loop.