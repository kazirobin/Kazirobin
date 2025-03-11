# Var, Let, and Const

In software, a variable is a symbolic name that represents a *value* or a *reference to a value*. It's a way to store information that can be reused and manipulated throughout your program. You can think of a variable like a label or even a sign pointer - it represents the data (which can potentially change) but is not the actual data itself. 

Variables are essential building blocks in JavaScript programming, allowing developers to store and manipulate data. There are 3 main ways to declare a variable, and your choice can have significant implications on your code's behavior and maintainability. Many developers just choose one and use it for everything, but that's just lazy and can sometimes cause problems.

Let's explore these three methods of variable declaration in JavaScript: `var`, `let`, and `const`, diving into when and why to use each, along with their respective advantages and drawbacks.

## **`var`: Function-Scoped Variables**

In JavaScript, `var` is a keyword used to declare a variable. It has some specific behaviors that set it apart from other variable declaration keywords like `let` and `const`.

Here's what you need to know about `var`:

1. **Function Scope**: Variables declared with `var` are function-scoped, meaning they are accessible within the function where they were declared (or globally if declared outside any function).
2. **Hoisting**: Unlike `let` and `const`, variables declared with `var` are "hoisted" to the top of their containing function or global scope. This means that they are technically available from the beginning of that scope, but their value will be `undefined` until the code where they are assigned is executed.
3. **Reassignment**: You can reassign new values to a variable declared with `var`.
4. **Redeclaration**: In non-strict mode, you can redeclare a variable using `var` in the same scope without getting an error, which is not allowed with `let` and `const`.
5. **No Block Scope**: `var` does not respect block scope (such as inside an `if` statement or a loop), which can sometimes lead to unexpected behavior. If you declare a variable with `var` inside a block, it's actually available to the entire surrounding function or global scope.

Because of these peculiarities, and with the introduction of `let` and `const` in ES6 (ECMAScript 2015), the use of `var` has become less common in modern JavaScript, and it's often recommended to use `let` or `const` instead for clearer scoping rules and better maintainability.

**Example**

```jsx
function varExample() {
  console.log(x); // undefined, because of hoisting
  var x = 10;
  console.log(x); // Output: 10
  
  if (true) {
    var x = 20; // Same variable, even though it's in a different block
  }
  
  console.log(x); // Output: 20, because var does not have block scope
}
```

## `let`: Block-Scoped Variables

So, if we had `var`, why did we need something else? The reason why the `let` keyword was introduced to javascript was because *function* scope is confusing and this led to a number of bugs and errors. `let` was was introduced in ES6 (ECMAScript 2015) as an alternative to var, with some key differences in behavior:

1. **Block Scope**: Unlike var, variables declared with let are block-scoped, meaning they are only accessible within the block in which they were declared (e.g., inside an if statement or a loop).
2. **No Hoisting**: Although let declarations are hoisted, the variables are not initialized until the code execution reaches the declaration. Attempting to access the variable before its declaration will result in a ReferenceError.
3. **Reassignment**: Like var, you can reassign new values to a variable declared with let.
4. **No Redeclaration**: In strict mode, you cannot redeclare a variable using let in the same scope.

**Example**

```jsx
function letExample() {
	console.log(x); // ReferenceError, because it doesn't exist yet (no hoisting)
	let x = 10;

	if (true) {
  		let x = 20; // Different variable because it's in a different block
  		let y = "I see how it works";
	}
	
	console.log(x); // Output: 10, because we are in the block for the original variable
	console.log(y); // ReferenceError, because y is block-scoped
}
```

## `const`: Block-Scoped Immutable References

The `const` keyword, which, like `let`, was introduced in ES6 (ECMAScript 2015). It has similarities to `let`, but with some unique characteristics:

1. **Block Scope**: Just like `let`, variables declared with `const` are block-scoped.
2. **No Hoisting**: Similar to `let`, `const` declarations are hoisted, but accessing them before their declaration in the code results in a ReferenceError.
3. **No Reassignment**: Unlike `var` and `let`, once a variable is assigned with `const`, it cannot be reassigned. Attempting to do so will result in a TypeError.
4. **No Redeclaration**: You cannot redeclare a variable using `const` in the same scope.
5. **Must Be Initialized**: A `const` declaration must be initialized with a value at the time it's declared.

**Example**

```jsx
function constExample() {
	if (true) {
		console.log(PI); // ReferenceError, because it doesn't exist yet (no hoisting)
		const PI = 3.14159;
		PI = 3; // Error: Assignment to constant variable
	}
	console.log(PI); // ReferenceError, because PI is block-scoped
	
	const obj = { value: 5 };
	obj.value = 10; // This is fine because object properties can be changed
	obj = { value: 20 }; // TypeError, reassignment not allowed
}
```