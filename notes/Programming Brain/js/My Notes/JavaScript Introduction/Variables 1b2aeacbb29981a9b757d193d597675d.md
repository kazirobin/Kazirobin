# Variables

`CreatedAt- 05 Jan 2024 / RevisedAt- 14 Nov 2024`

A JavaScript variable is simply the name of the storage location. There are two types of variables in JavaScript: local variable and global variable. There are some rules while declaring a JavaScript variable (also known as identifiers).

---

## Declare Variables

In JavaScript, we use either `var` or `let` keyword to declare variables. For example,

```jsx
var x;
let y;
```

Here, `x` and `y` are variables.

## JavaScript var vs let

Both `var` and `let` are used to declare variables. However, there are some differences between them.

| var | let |
| --- | --- |
| `var` is used in the older versions of JavaScript | `let` is the new way of declaring variables starting ES6 (ES2015). |
| `var` is function scoped | `let` is block scoped |
| `var` variables can be re-declared and updated | `let` can be updated but not re-declared |
| For example, `var x`; | For example, `let y`; |

## JavaScript Initialize Variables

We use the assignment operator `=` to assign a value to a variable.

```jsx
let x;
x = 5;
```

Here, 5 is assigned to variable `x`.

You can also initialize variables during its declaration.

```jsx
let x = 5;
let y = 6;
```

In JavaScript, it's possible to declare variables in a single statement.

```jsx
let x = 5, y = 6, z = 7;
```

If you use a variable without initializing it, it will have an `undefined` value.

```jsx
let x; // x is the name of the variable

console.log(x); // undefined
```

Here `x` is the variable name and since it does not contain any value, it will be undefined.

## Change the Value of Variables

It's possible to change the value stored in the variable. For example,

```jsx
// 5 is assigned to variable x
let x = 5; 
console.log(x); // 5

// value of variable x is changed
x = 3; 
console.log(x); // 3
```

## JavaScript Constants

The `const` keyword was also introduced in the ES6(ES2015) version to create constants. For example,

```jsx
const x = 5;
```

Once a constant is initialized, we cannot change its value.

```jsx
const x = 5;
x = 10;  // Error! constant cannot be changed.
console.log(x)
```

Simply, a constant is a type of variable whose value cannot be changed.

Also, you cannot declare a constant without initializing it. For example,

```jsx
const x;  // Error! Missing initializer in const declaration.
x = 5;
console.log(x)
```