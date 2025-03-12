# This Keyword

The keyword `this` refers to the value of the object that is bound to the function at the time of its call, meaning that its value is different depending on whether a function is called as a method, as a standalone function, or as a constructor.

## Where it is called

When `this` is used alone, `this` refers to the global object (`window` object in browsers). For example,

```jsx
let a = this;
console.log(a);  // Window {}

this.name = 'Hossain';
console.log(window.name); // Hossain
```

Here, `this.name` is the same as `window.name`

## Inside Function

When `this` is used in a function, `this` refers to the global object (`window` object in browsers). For example,

```jsx
function greet() {

    // this inside function
    // this refers to the global object
    console.log(this);
}

greet(); // Window {}
```

## Inside Constructor Function

In JavaScript, constructor functions are used to create objects. When a function is used as a constructor function, `this` refers to the object inside which it is used. For example,

```jsx
function Person() {

    this.name = 'Hossain';
    console.log(this);

}

let person1 = new Person();

console.log(person1.name);
```

### Output

```jsx
Person {name: "Hossain"}

Hossain
```

Here, `this` refers to the person1 object. That's why, `person1.name` gives us `Hossain`.

**Note:** When `this` is used with ES6 classes, it refers to the object inside which it is used (similar to constructor functions).

## Inside Object Method

When `this` is used inside an object's method, `this` refers to the object it lies within. For example,

```jsx
const person = {
    name : 'Hossain',
    age: 25,

    // this inside method
    // this refers to the object itself
    greet() {
        console.log(this);
        console.log(this.name);
    }
}

person.greet();
```

### Output

```jsx
{name: "Hossain", age: 25, greet: ƒ}

Hossain
```

In the above example, `this` refers to the `person` object.

## Inside Inner Function

When you access `this` inside an inner function (inside a method), `this` refers to the global object. For example,

```jsx
const person = {
    name : 'Hossain',
    age: 25,

    // this inside method
    // this refers to the object itself
    greet() {
        console.log(this);        // {name: "Hossain", age ...}
        console.log(this.age);  // 25

        // inner function
        function innerFunc() {
        
            // this refers to the global object
            console.log(this);       // Window { ... }
            console.log(this.age);    // undefined
            
        }

        innerFunc();

    }
}

person.greet();
```

### Output

```jsx
{name: "Hossain", age: 25, greet: ƒ}
25
Window { …}
undefined
```

Here, `this` inside `innerFunc()` refers to the **global object** because `innerFunc()` is inside a method.

However, `this.age` outside `innerFunc()` refers to the `person` object.

## Inside Arrow Function

Inside the arrow function, `this` refers to the parent scope. For example,

```jsx
const greet = () => {
    console.log(this);
}
greet(); // Window {...}
```

Arrow functions do not have their own `this`. When you use `this` inside an arrow function, `this` refers to its parent scope object. For example,

```jsx
const greet = {
    name: 'Hossain',

    // method
    sayHi () {
        let hi = () => console.log(this.name);
        hi();
    }
}

greet.sayHi(); // Hossain
```

Here, `this.name` inside the `hi()` function refers to the `greet` object.

You can also use the arrow function to solve the issue of having `undefined` when using a function inside a method (as seen in Example Above). For example,

```jsx
const person = {
    name : 'Hossain',
    age: 25,

    // this inside method
    // this refers to the object itself
    greet() {
        console.log(this);
        console.log(this.age);

        // inner function
        let innerFunc = () => {
        
            // this refers to the global object
            console.log(this);
            console.log(this.age);
            
        }

        innerFunc();

    }
}

person.greet();
```

### Output

```jsx
{name: "Hossain", age: 25, greet: ƒ}
25
{name: "Hossain", age: 25, greet: ƒ}
25
```

Here, `innerFunc()` is defined using the arrow function. It takes `this` from its parent scope. Hence, `this.age` gives **25**.

When the arrow function is used with `this`, it refers to the outer scope.

## Inside Function with Strict Mode

When `this` is used in a function with strict mode, `this` is undefined. For example,

```jsx
'use strict';
this.name = 'Hossain';
function greet() {

    // this refers to undefined
    console.log(this);
}
greet(); // undefined
```

**Note:** When using `this` inside a function with strict mode, you can use JavaScript Function call().

For example,

```jsx
'use strict';
this.name = 'Hossain';

function greet() {
    console.log(this.name);
}

greet.call(this); // Jack
```

When you pass `this` with the `call()` function, `greet()` is treated as the method of the `this` object (global object in this case).s