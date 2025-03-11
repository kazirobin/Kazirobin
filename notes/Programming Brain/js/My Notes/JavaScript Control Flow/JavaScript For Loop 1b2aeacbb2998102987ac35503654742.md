# JavaScript For Loop

The JavaScript `for` loop iterates the elements for the fixed number of times. It should be used if number of iteration is known. The syntax of for loop is given below.

```jsx
for (initialExpression; condition; updateExpression) {
    // for loop body
}
```

Here,

1. The **initialExpression** initializes and/or declares variables and executes only once.
2. The **condition** is evaluated.
- If the condition is `false`, the `for` loop is terminated.
- If the condition is `true`, the block of code inside of the `for` loop is executed.
1. The **updateExpression** updates the value of **initialExpression** when the condition is `true`.
2. The **condition** is evaluated again. This process continues until the condition is `false`.

Example,

```jsx
// program to display text 5 times
const num = 5;

// looping from i = 1 to 5
for (let i = 1; i <= num; i++) {
    console.log(`I love JavaScript.`);
}
```

Here is how this program works.

| Iteration | Variable | Condition: i <= n | Action |
| --- | --- | --- | --- |
| 1st | `i = 1` and `n = 5` | `true` | I love JavaScript. |
| 2nd | `i = 2` and `n = 5` | `true` | I love JavaScript. |
| 3rd | `i = 3` and `n = 5` | `true` | I love JavaScript. |
| 4th | `i = 4` and `n = 5` | `true` | I love JavaScript. |
| 5th | `i = 5` and `n = 5` | `true` | I love JavaScript. |
| 6th | `i = 6` and `n = 5` | `false` | The loop is terminated. |

## For Loop Break Statement

The `break` statement enables us to immediately exit a loop without executing any of the remaining code in the loop. Typically, we use break statements with a conditional because we want to exit the loop when a specific condition is met. At a high level, a `break` statement may look like this:

```jsx
let content = "";
let i;

for (i = 1; i < 1000; i++) {
    if (i === 6) {
        break;
    }
    content += "I love JavaScript " + i + "\n";
}
console.log(content);
```

## For Loop Continue Statement

While the `break` statement immediately exits the loop, the `continue` statement immediately returns to the condition of the loop. This enables us to skip specific iterations of the loop without exiting the entire loop. Take a look at the example program below.

```jsx
let content = "";
let i;

for (i = 1; i < 7; i++) {
    if (i === 4) {
        continue;
    }
    content += "I love JavaScript " + i + "\n";
}
console.log(content);
```