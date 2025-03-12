# Execution Context

JavaScript is a single-threaded interpreted language. Every browser has its own JavaScript engine. Google Chrome has the V8 engine, Mozilla Firefox has SpiderMonkey, and so on. They all are used for the same goal, because the browsers cannot directly understand JavaScript code.

## What is the Execution Context?

When the JavaScript engine scans a script file, it makes an environment called the **Execution Context** that handles the entire transformation and execution of the code.

During the context runtime, the parser parses the source code and allocates memory for the variables and functions. The source code is generated and gets executed.

There are two types of execution contexts `global` and `function`. The global execution context is created when a JavaScript script first starts to run, and it represents the global scope in JavaScript. A function execution context is created whenever a function is called, representing the function's local scope.

## Phases of the JavaScript Execution Context

There are two phases of JavaScript execution context:

1. **Creation phase**: In this phase, the JavaScript engine creates the execution context and sets up the script's environment. It determines the values of variables and functions and sets up the scope chain for the execution context.
2. **Execution phase**: In this phase, the JavaScript engine executes the code in the execution context. It processes any statements or expressions in the script and evaluates any function calls.

Everything in JS happens inside this execution context. It is divided into two components. One is memory and the other is code. It is important to remember that these phases and components are applicable to both global and functional execution contexts.

Let’s start with the following example:

```bash
let x = 10;

function timesTen(a){
    return a * 10;
}

let y = timesTen(x);

console.log(y); // 100
```

In this example:

- First, declare the `x` variable and initialize its value with `10`.
- Second, declare the `timesTen()` function that accepts an argument and returns a value that is the result of the multiplication of the argument with `10`.
- Third, call the `timesTen()` function with the argument as the value of the `x` variable and store result in the variable `y`.
- Finally, output the variable `y` to the Console.

Behind the scenes, JavaScript does many things. in this tutorial, you will focus on execution contexts.

Each execution context has two phases: the creation phase and the execution phase.

## The creation phase

When the JavaScript engine executes a script for the first time, it creates the global execution context. During this phase, the JavaScript engine performs the following tasks:

- Create the global object i.e., `window` in the web browser or `global` in Node.js.
- Create the `this` object and bind it to the global object.
- Set up a memory heap for storing variables and function references.
- Store the function declarations in the memory heap and variables within the global execution context with the initial values as `undefined`.

When the JavaScript engine executes the code example above, it does the following in the creation phase:

- First, store the variables `x` and `y` and function declaration `timesTen()` in the global execution context.
- Second, initialize the variables `x` and `y` to `undefined`.

![javascript-execution-context-global-execution-context-in-creation-phase.png](Execution%20Context%201b2aeacbb29981919aaee90dc77c6fd7/javascript-execution-context-global-execution-context-in-creation-phase.png)

After the creation phase, the global execution context moves to the execution phase.

## The execution phase

During the execution phase, the JavaScript engine executes the code line by line, assigns the values to variables, and executes the function calls.

![javascript-execution-context-global-execution-context-in-execution-phase.png](Execution%20Context%201b2aeacbb29981919aaee90dc77c6fd7/javascript-execution-context-global-execution-context-in-execution-phase.png)

For each function call, the JavaScript engine creates a new **`function execution context`**.
The function execution context is similar to the global execution context. But instead of creating the global object, the JavaScript engine creates the `arguments` object that is a reference to all the parameters of the function:

![javascript-execution-context-function-execution-context-in-creation-phase.png](Execution%20Context%201b2aeacbb29981919aaee90dc77c6fd7/javascript-execution-context-function-execution-context-in-creation-phase.png)

In our example, the function execution context creates the `arguments` object that references all parameters passed into the function, sets `this` value to the global object, and initializes the `a` parameter to `undefined`.

During the execution phase of the function execution context, the JavaScript engine assigns `10` to the parameter `a` and returns the result (`100`) to the global execution context:

![javascript-execution-context-function-execution-context-in-execution-phase.png](Execution%20Context%201b2aeacbb29981919aaee90dc77c6fd7/javascript-execution-context-function-execution-context-in-execution-phase.png)

To keep track of all the execution contexts, including the global execution context and function execution contexts, the JavaScript engine uses the call stack.