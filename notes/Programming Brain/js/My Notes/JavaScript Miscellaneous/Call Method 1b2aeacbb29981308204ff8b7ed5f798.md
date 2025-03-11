# Call Method

The **call() method** is a predefined JavaScript method. It can be used to invoke (call) a method with an owner object as an argument (parameter). This allows borrowing methods from other objects, executing them within a different context, overriding the default value, and passing arguments.

```jsx
//function that adds two numbers 
function sum(a, b) {
  return a + b;
}

// calling sum() function  
var result = sum.call(this, 5, 10);

console.log(result);

//Output:
// 15
```

## Call Syntax

The syntax of the `call()` method is:

```jsx
func.call(thisArg, arg1, ... argN)
```

Here, `func` is a function.

## Call **Parameters**

The `call()` method can take **two** parameters:

- `thisArg` - The `thisArg` is the object that the `this` object references inside the function `func`.
- `arg1, ... argN` (optional) - Arguments for the function `func`.

**Note:** By default, in a function `this` refers to the global object i.e, window in web browsers and `global` in node.js.

## Using Call Method

```jsx
function sum(a, b) {
  return a + b;
}

// invoking sum() by passing this and 'a', 'b' arguments 
let result = sum.call(this, 5, 3);

console.log(result);
```

In the above example, we have defined a function `sum()` that returns the sum of two numbers.
We have then used the `call()` method to call `sum()` as `sum.call(this, 5, 3)`.

Here, by default, the `this` inside the function is set to the global object.

## With & Without Using Call Method

```jsx
// function that finds product of two numbers
function product(a, b) {
  return a * b;
}

// invoking product() without using call() method
let result1 = product(5, 2);

console.log("Return value Without using call() method: " + result1);

// invoking product() using call() method
let result2 = product.call(this, 5, 2);

console.log("Return value Using call() method: " + result2);
```

### Output

```jsx
Return value Without using call() method: 10
Return value Using call() method: 10
```

In the above example, we have called the `product()` function: without using `call()` and using `call()`.

- Without using `call()`we can directly invoke `product()` as `product(5, 2)`.
- Using `call()`we have to pass `this` argument as `product.call(this, 5, 2)`.

## Passing Object as this Value in Call Method

```jsx
// object definition
const human = {
  firstName: "Hossain",
  lastName: "Palin",
  age: 26,
};

// function definition
function greet() {
  const string = `My name is ${this.firstName} ${this.lastName}. I am ${this.age} years old.`;
  console.log(string);
}

// passing object as this value in call() method
greet.call(human);
```

### Output

```jsx
My name is Hossain Palin. I am 26 years old.
```

In the above example, we have defined the `greet()` function inside which we have defined a variable string that can access the values of human.

We have then passed the human object as `this` value in the `call()` method as `greet.call(human)`, which calls `greet()`.

## Using Call Method to Chain Constructors

```jsx
//function definition 
function Animal(name, age) {
  this.name = name;
  this.age = age;
}

//function definition 
function Horse(name, age) {
  Animal.call(this, name, age);
  this.sound = "Neigh";
}

//function definition 
function Snake(name, age) {
  Animal.call(this, name, age);
  this.sound = "Hiss";
}

const snake1 = new Snake("Harry", 5);
console.log(snake1.name, snake1.age, snake1.sound);

const horse1 = new Horse("Arnold", 8);
console.log(horse1.name, horse1.age, horse1.sound);
```

### Output

```jsx
Harry 5 Hiss
Arnold 8 Neigh
```

**Note:** The difference between `call()` and `apply()` is that `call()` accepts an argument list, while `apply()` accepts a single array of arguments.