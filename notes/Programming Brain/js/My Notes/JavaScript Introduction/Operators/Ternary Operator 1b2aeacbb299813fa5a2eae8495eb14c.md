# Ternary Operator

A ternary operator can be used to replace an `if..else` statement in certain situations. The ternary operator is a conditional operator that evaluates either of two expressions – a true expression and a false expression – based on a conditional expression that you provide.

Here's the syntax:

```jsx
condition ? **expression1** : **expression2**
```

The ternary operator evaluates the test condition.

- • If the condition is `true`, **expression1** is executed.
- • If the condition is `false`, **expression2** is executed.

The ternary operator takes three operands, hence, the name ternary operator. It is also known as a conditional operator.

Let's write a program to determine if a student passed or failed in the exam based on marks obtained.

```jsx
let marks = prompt('Enter your marks :');

// check the condition
let result = (marks >= 33) ? 'pass' : 'fail';

console.log(`You ${result} the exam.`);
```

Output 1

```
Enter your marks: 80
You pass the exam.
```

Suppose the user enters **80**. Then the condition `marks >= 33` is checked which evaluates to `true`. So the first expression `pass` is assigned to the `result` variable.

Output 2

```
Enter your marks: 30
You fail the exam.
```

Suppose the use enters **30**. Then the condition `marks >= 33` evaluates to `false`. So the second expression `fail` is assigned to the `result` variable.