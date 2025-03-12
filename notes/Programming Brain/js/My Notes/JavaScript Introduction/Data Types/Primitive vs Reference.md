# Primitive vs. Reference

In the vast landscape of JavaScript, understanding data types is fundamental to mastering the language. JavaScript, as a dynamically typed language, relies on data types to categorize and process information efficiently. It’s like having a toolbox with different types of tools, each designed for specific tasks.

## The World of Data Types

Data types are the building blocks of any programming language. They define the nature of the data we work with and how that data is stored, manipulated, and interacted with in our code. JavaScript offers a diverse range of data types, and at a high level, they can be categorized into two broad groups: primitive types and reference types.

Primitive values are atomic pieces of data while reference values are objects that might consist of multiple values.

## Stack and Heap Memory

When you declare variables, the JavaScript engine allocates the memory for them on two memory locations: stack and heap.

Static data is the data whose size is fixed at compile time. Static data includes:

- Primitive values (null, undefined, boolean, number, string, symbol, and BigInt)
- Reference values that refer to objects.

Because static data has a size that does not change, the JavaScript engine allocates a fixed amount of memory space to the static data and stores it on the stack.

For example, the following declares two variables and initializes their values to a literal string and a number:

```jsx
let name = 'John';
let age = 25;
```

Because `name` and `age` are primitive values, the JavaScript engine stores these variables on the stack as shown in the following picture:

![JavaScript-stack-memory.svg](Primitive%20vs%20Reference%201b2aeacbb29981d2ac8cc6039c4a0d73/JavaScript-stack-memory.svg)

**Note:** Strings are objects in many programming languages, including Java and C#. However, strings are primitive values in JavaScript.

Unlike the stack, JavaScript stores objects (and functions) on the heap. The JavaScript engine doesn’t allocate a fixed amount of memory for these objects. Instead, it’ll allocate more space as needed.

The following example defines the `name`, `age`, and `person` variables:

```jsx
let name = 'John';
let age = 25;

let person = {
  name: 'John',
  age: 25,
};
```

Internally, the JavaScript engine allocates the memory as shown in the following picture:

![JavaScript-heap-memory.svg](Primitive%20vs%20Reference%201b2aeacbb29981d2ac8cc6039c4a0d73/JavaScript-heap-memory.svg)

In this picture, JavaScript allocates memory on the stack for the three variables `name`, `age`, and `person`.

The JavaScript engine creates a new object on the heap memory. Also, it links the `person` variable on the stack memory to the object on the heap memory.

Because of this, we say that the `person` variable is a reference that refers to an object.

## Dynamic Properties

A reference value allows you to add, change, or delete properties at any time. For example:

```jsx
let person = {
  name: 'John',
  age: 25,
};

// add the ssn property
person.ssn = '123-45-6789';

// change the name
person.name = 'John Doe';

// delete the age property
delete person.age;

console.log(person);
```

**Output**

```jsx
{ name: 'John Doe', ssn: '123-45-6789' }
```

Unlike a reference value, a primitive value cannot have properties. This means that you cannot add a property to a primitive value.

JavaScript allows you to add a property to a primitive value. However, it won’t take any effect. For example:

```jsx
let name = 'John';
name.alias = 'Knight';

console.log(name.alias); // undefined
```

**Output**

```jsx
undefined
```

In this example, we add the `alias` property to the `name` primitive value. But when we access the `alias` property via the `name` primitive value, it returns `undefined`.

## Copying Values

When you assign a primitive value from one variable to another, the JavaScript engine creates a copy of that value and assigns it to the variable. For example:

```jsx
let age = 25;
let newAge = age;
```

In this example:

- First, declare a new variable `age` and initialize its value with `25`.
- Second, declare another variable `newAge` and assign the `age` to the `newAge` variable.

Behind the scenes, the JavaScript engine creates a copy of the primitive value `25` and assign it to the `newAge` variable.

The following picture illustrates the stack memory after the assignment:

![JavaScript-copy-a-primitive-value.svg](Primitive%20vs%20Reference%201b2aeacbb29981d2ac8cc6039c4a0d73/JavaScript-copy-a-primitive-value.svg)

On the stack memory, the `newAge` and `age` are separate variables. If you change the value of one variable, it won’t affect the other.

For example:

```jsx
let age = 25;
let newAge = age;

newAge = newAge + 1;
console.log(age, newAge);
```

![JavaScript-change-a-primitive-value.svg](Primitive%20vs%20Reference%201b2aeacbb29981d2ac8cc6039c4a0d73/JavaScript-change-a-primitive-value.svg)

When you assign a reference value from one variable to another, the JavaScript engine creates a reference so that both variables refer to the same object on the heap memory. This means that if you change one variable, it’ll affect the other.

For example:

```jsx
let person = {
  name: 'John',
  age: 25,
};

let member = person;

member.age = 26;

console.log(person);
console.log(member);
```

## How it works

First, declare a `person` variable and initialize its value with an object with two properties `name` and `age`.

Second, assign the `person` variable to the `member` variable. In the memory, both variables reference the same object, as shown in the following picture:

![JavaScript-copy-a-reference-value.svg](Primitive%20vs%20Reference%201b2aeacbb29981d2ac8cc6039c4a0d73/JavaScript-copy-a-reference-value.svg)

Third, change the `age` property of the object via the `member` variable:

![JavaScript-change-a-reference-value.svg](Primitive%20vs%20Reference%201b2aeacbb29981d2ac8cc6039c4a0d73/JavaScript-change-a-reference-value.svg)

Since both `person` and `member` variables reference the same object, changing the object via the `member` variable is also reflected in the `person` variable.