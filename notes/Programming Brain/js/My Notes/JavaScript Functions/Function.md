# Function

Functions are essential building blocks in JavaScript, they are packed with logic for performing tasks. A function can be likened to a procedure that performs a task or calculates a value.

---

## Different methods of declaring a JavaScript function

In JavaScript, there are different ways of declaring functions. Let’s examine what a function declaration is.

A function declaration, also known as a function definition or statement, is a way of providing sets of instructions to be carried out in a program when executed. It is a way of saving a function with a particular parameter so it can be called (invoked) when needed to perform the task for which it was defined.

The syntax (as seen below) of a function must be defined before it can be implemented:

```jsx
function name() {
    // body content
}
```

Let’s examine the example above:

1. The F**unction** is a keyword that precedes the actual code. It is a **Statement Identifier**. This is why a function is said to be self-contained.
2. **Name** is the name of the function to be executed on the parameters. It is user-defined and must be an action word.
3. **( )** is the grouping operator which is a pair of parentheses and it is what envelopes the arguments that are to be run in the program.
4. **{ }** is the block that houses the code itself. It is the real definition of a function and is used to group statements.

The declared function can be invoked with **name ( )**; when required.

An example of a function statement is shown below:

```jsx
function greet() {
    console.log("Hello world");
}
greet();
```

Now that we know what a function declaration is, we can then consider the different ways a function can be declared in JavaScript:

## Function Expression

A function can be declared using a function expression. It is declared quite differently from the general syntax because it uses a variable to denote the name of the function. This variable comes before the keyword `function`. The function is invoked by calling out the variable with trailing parenthesis and semicolons:

```jsx
var greet = function () {
  console.log("Welcome to Javascript");
};
greet();
```

This method of function declaration makes tracing bugs easy. It specifies the name of the function in the stack trace. A function declaration through the function expression method can be used both as anonymous functions and IIFE (immediately invoked function expressions).

## Anonymous Function

Anonymous function declaration allows function names to appear hidden in the declaration itself. The function name is attached to the function keyword in the general function declaration syntax, but an anonymous function is declared using only the function keyword and a parenthesis.

```jsx
function  () {
  // function body
}
```

This function is declared only once because and cannot be recalled without an identifier. The only way it can be recalled is to assign the function to a variable so that the variable name can be invoked in our code.

For instance, the example below shows an anonymous function declaration that is assigned to a variable `greet`. From the example, variable `greet` stores the function, and anytime we want to invoke the function we simply call `greet()`:

```jsx
var greet = function () {
    console.log("Welcome to Javascript");
};
greet();
```

An anonymous function can also be an argument of a function hence, it can be declared inside another function as its parameters. A simple example to illustrate is a native JavaScript function `setTimeout`

```jsx
setTimeout(
  function () {
    console.log("Executed after three seconds");
  }  , 2000 // delay in milliseconds
)
```

## Immediately Invoked Function Expressions

IIFE are functions that can be stated as expressions or normal declarations and use the anonymous property of the function expression to execute its code. If you want to execute a function immediately after the declaration, use IIFE. This is executed by wrapping the anonymous function in parentheses and ending it with a semicolon

```jsx
(function () {
  console.log("Welcome to Javascript");
})();
```

The trailing parentheses `(  )` are used to invoke the function. IIFE is mostly used to avoid pollution of the global objects. For instance, in a case where two JavaScript files containing the same functions are loaded into a single HTML file, the later identifier from IIFE overrides the foremost.

Although not very common, IIFE can be created with unary operators. However, these operators can affect the returned value of IIFE. Below is a list of unary operators and how they affect IIFE

```jsx
+function(){
   return 2;
}();//This will return 2

-function(){
   return 2;
}();//This will return -2

~function(){
   return 2;
}();//This will return -3

!function(){
   return 2;
}();//This will return false
```

## Constructor Functions

The concept of a function constructor is to create a function object which executes in the global scope. It can be used to create multiple objects that are similar. The function constructor has similar functionalities as the function expression. A constructor function is called with the `new` keyword to create an object. The `Function( )` is the constructor which houses the arguments

```jsx
var F = new Function(arg1, functionBody)
var F = new Function(arg1, arg2, functionBody)
var F = new Function(arg1, arg2, .........., argN, functionBody)
```

In the example below, we have created a function multiply with the new keyword. Then, we can invoke the `function` we declared by calling `multiply( )`

```jsx
// new Function creates a new function object 'multiply'
const multiply = new Function('a', 'b', 'return a * b');

console.log(multiply(2, 6));
// expected output: 12
```

Also, constructor functions can be used with the `this` keyword. This allows developers to assign values to the function object as properties. For example, in the code below, the properties `name` and `age` are assigned to the function `Person` using the `this` keyword.

```jsx
// constructor function
function Person() {
    this.name = "Anita",
    this.age = 21
}
// create an object
const person = new Person();

//access properties
console.log(person.name);
console.log(person.age);
```

## Hoisting

With JavaScript functions, it is possible to call functions before actually writing the code for the function statement and they give a defined output. This property is called hoisting. Hoisting is the ability of a function to be invoked at the top of the script before it is declared. Since the function is hoisted at the top of the block but not initialized, it cannot be used until it has been declared. Recalling earlier examples.

```jsx
greet();

function greet() {
    console.log("Hello world");
}
```

This is a function declaration that has been hoisted and when executed by the browser outputs `Hello World`. `greet( )` is invoked before it is declared. However, there’ll be no error since `greet( )` will be stored at the heap until the `greet( )` function is initialized.

Hoisting operates on the mechanism of scope and variables used to identify function expressions are all based on the scope of the JavaScript engine which executes before initializing a function.

## Arrow Function

This is a feature available in the ES6 version of JavaScript and as such has not stayed in the space for as long as the other features in the function declaration. It is generally a cleaner way of creating JavaScript functions and it is similar to the function expression.

```jsx
let name = (arguements1, arguements2, arguements 3...) => {
    statements
};
```

It does not use the function keyword in its syntax. For multiple-line statements, curly brackets are used. The arrow function statement can implicitly return values. This means that the word `return` isn’t needed in some cases to return the value of a function. The example below explains this.

```jsx
const greet = () => "Hello World"

greet() // Hello World
```

However, there are cases where the arrow function statement is explicitly returned. For instance, when a curly bracket is wrapped around a function body, it doesn’t return a value implicitly. This means you have to use the `return` keyword. A simple example to illustrate this is below.

```jsx
let sum = (x, y) => {
    let result = x + y
    return result;
}
let result1 = sum(2, 3);
console.log(result1);
```