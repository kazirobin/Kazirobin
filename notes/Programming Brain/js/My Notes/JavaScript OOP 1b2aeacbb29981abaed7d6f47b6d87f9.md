# JavaScript OOP

`CreatedAt- 28 Sep 2024 / RevisedAt-`

Object-Oriented Programming is a programming style based on classes and objects. These group data (properties) and methods (actions) inside a box.

OOP was developed to make code more flexible and easier to maintain.

JavaScript is prototype-based procedural language, which means it supports both functional and object-oriented programming.

## What is a Class?

You can think of a class like a blueprint of a house. A class is not a real world object but we can create objects from a class. It is like an template for an object.

We can create classes using the `class` keyword which is reserved keyword in JavaScript. Classes can have their own properties and methods. We will study how to create a class in detail shortly. This is just a high level overview of a class.

Let's take an example. Below is a blueprint for a house (like a class).

## What is an Object?

An object is an instance of a class. Now with the help of the house class we can construct a house. We can construct multiple houses with the help of same house class.

## Example of Classes and Objects in Action

Let's take a simple example to understand how classes and objects work.

The below example has nothing to do with JavaScript syntax. It is just to explain classes and objects. We will study the syntax of OOP in JavaScript in a bit.

Consider a Student class. Student can have properties like name, age, standard, and so on, and functions like study, play, and do home work.

```jsx
class Student {
  constructor(name, age, standard) {
    this.name = name;
    this.age = age;
    this.standard = standard;
  }

  // Methods (Action)
  study() {
    console.log(`${this.name} is studying`);
  }

  Play() {
    console.log(`${this.name} is playing`);
  }

  doHomeWork() {
    console.log(`${this.name} is doing homework`);
  }
}
```

With the help of the above class, we can have multiple students or instances.

### **Here's info for** `**Student - 01**`**:**

```jsx
class Student {
  constructor(name, age, standard) {
    this.name = name;
    this.age = age;
    this.standard = standard;
  }

  // Methods (Action)
  study() {
    console.log(`${this.name} is studying`);
  }

  Play() {
    console.log(`${this.name} is playing`);
  }

  doHomeWork() {
    console.log(`${this.name} is doing homework`);
  }
}

// Creating an object of Student
let student1 = new Student("John", 15, 10);
```

### **Here's info for** `**Student - 02**`**:**

```jsx
class Student {
  constructor(name, age, standard) {
    this.name = name;
    this.age = age;
    this.standard = standard;
  }

  // Methods (Action)
  study() {
    console.log(`${this.name} is studying`);
  }

  Play() {
    console.log(`${this.name} is playing`);
  }

  doHomeWork() {
    console.log(`${this.name} is doing homework`);
  }
}

// Creating an object of Student
let student2 = new Student("Alice", 12, 7);
```

## How Do We Actually Design a Class?

There is no perfect answer to this question. But we can get help from some OOP principles when designing our classes.

There are 4 main principles in OOP, and they are:

[Abstraction](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/Abstraction%201b2aeacbb2998146b5cec3eedc460617.md)

[Encapsulation](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/Encapsulation%201b2aeacbb299810c8581dd0ac6e2f941.md)

[Inheritance](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/Inheritance%201b2aeacbb29981f9b3a4cd1323cfeb2e.md)

[Polymorphism](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/Polymorphism%201b2aeacbb29981519243cc1e838a8447.md)

## What is Prototypal Inheritance in JavaScript?

You have likely already used Prototypal Inheritance without knowing it – for example, if you've used methods on arrays like push(), pop(), map() and so on (which are available on all arrays).

Just like Array.prototype we will create our own prototypes and this will help you understand JavaScript inside out.

![ss.png](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/ss.png)

There are three main ways to implement Prototypal Inheritance in JavaScript:

[**Constructor Functions**](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/Constructor%20Functions%201b2aeacbb2998107974af0c66e434893.md)

[**ES6 Classes**](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/ES6%20Classes%201b2aeacbb29981ba88f2f099480d6d9d.md)

[**Object.create()**](JavaScript%20OOP%201b2aeacbb29981abaed7d6f47b6d87f9/Object%20create()%201b2aeacbb29981e18f58c994eaa0694c.md)

## How Encapsulation Works in JavaScript

Above, we looked at what encapsulation means at a very high level. Now we will look at an example to explain it more thoroughly.

Encapsulation can be defined as *“the packing of data and functions into one component”.* This is also known as grouping or bundling, and simply means to bring together data and the methods which operate on data. It can be a function, a class, or an object.

Encapsulation enables “*controlling access to that component*”. When we have the data and related methods in a single unit, we can control how is it accessed outside the unit. This process is called Encapsulation**.**

### Protected properties

```jsx
class User{
    constructor(name, password){
        this._name = name
        this._password = password
    }
}

const kedar = new User("kedar", 123456)
console.log(kedar._password);
```

A protected member is accessible within the class and any object that inherits from it. A protected value is shared across all layers of the prototype chain.

We used (_) in `this._name` , which is a protected property. We can still access this property outside of the class. This is just a convention programmers use.

If we know there is (_) in a property name we are not supposed to manipulate that property from outside the class.

```jsx
class User{
    constructor(name, password){
        this._name = name
        this._password = password
    }

    get getName(){
        console.log(this._name)
    }
}

const kedar = new User("kedar", 123456)
kedar.getName
```

### Private properties

```jsx
class User{
    constructor(name, password){
        this.#name = name
        this._password = password
    }

    get getName(){
        console.log(this._name)
    }
}

const kedar = new User("kedar", 123456)
console.log(kedar.#name);
```

To implement a truly private property in JavaScript we have to use (#) before the property name or method. These private properties and methods will not be accessible from outside of class which will make them truly private.

This will help restrict accessing properties from outside of the class. If we want to access property from outside we have to make method which will only print properties without giving access to change value of that property.

```jsx
class User{
    #name

    constructor(name, password){
        this.#name = name
        this._password = password
    }

    #printName(){
        console.log(this.#name);
    }

    PrintFromPrivateMethod(){
        this.#printName()
    }
}

const kedar = new User("kedar", 123456)
kedar.PrintFromPrivateMethod()
```