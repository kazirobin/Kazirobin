# Data Types

JavaScript is a dynamically typed (also called loosely typed) scripting language. In JavaScript, variables can receive different data types over time. JavaScript provides different data types to hold different types of values. There are two types of data types in JavaScript.

---

## 1. Primitive Data Type

The predefined data types provided by JavaScript language are known as primitive data types. Primitive data types are also known as in-built data types.

Below is a list of Primitive Data Types with proper descriptions and examples:

### String Data Type

`String` is used to store text. In JavaScript, strings are surrounded by quotes:

- Single quotes: `'Hello'`
- Double quotes: `"Hello"`
- Backticks: `Hello`

For example,

```jsx
const name = 'hossain';
const name1 = "palin";
const result = `The names are ${name} and ${name1}`;
```

Single quotes and double quotes are practically the same and you can use either of them.

Backticks are generally used when you need to include variables or expressions into a string. This is done by wrapping variables or expressions with `${variable or expression}` as shown above and it is called JavaScript Template Literals.

### Number Data Type

`Number` represents integer and floating numbers (decimals and exponentials). For example,

```jsx
const number1 = 3;
const number2 = 3.433;
const number3 = 3e5 // 3 * 10^5
```

A number type can also be `+Infinity`, `Infinity`, and `NaN (not a number)`. For example,

```jsx
const number1 = 3/0;
console.log(number1); // Infinity

const number2 = -3/0;
console.log(number2); // -Infinity

// strings can't be divided by numbers
const number3 = "abc"/3; 
console.log(number3);  // NaN
```

### BigInt Data Type

In JavaScript, `Number` type can only represent numbers less than `($2^5$$^3$ - 1)` and more than - `($2^5$$^3$ - 1)`. However, if you need to use a larger number than that, you can use the `BigInt` data type.

A `BigInt` number is created by appending `n` to the end of an integer. For example,

```jsx
// BigInt value
const value1 = 900719925124740998n;

// Adding two big integers
const result1 = value1 + 1n;
console.log(result1); // "900719925124740999n"

const value2 = 900719925124740998n;

// Error! BitInt and number cannot be added
const result2 = value2 + 1; 
console.log(result2);
```

Output

```jsx
900719925124740999n
Uncaught TypeError: Cannot mix BigInt and other types
```

### Boolean Data Type

This data type represents logical entities. `Boolean` represents one of two values: `true` or `false`. It is easier to think of it as a yes/no switch. For example,

```jsx
const dataChecked = true;
const valueCounted = false;
```

### Undefined Data Type

The `undefined` data type represents the **value that is not assigned**. If a variable is declared but the value is not assigned, then the value of that variable will be `undefined`. For example,

```jsx
let name;
console.log(name); // undefined
```

It is also possible to explicitly assign a variable value `undefined`. For example,

```jsx
let name = undefined;
console.log(name); // undefined
```

### Null Data Type

In JavaScript, `null` is a special value that represents an empty or unknown value. For example,

```jsx
const number = null;
```

The code above suggests that the `number` variable is empty.

### Symbol Data Type

This data type was introduced in a newer version of JavaScript (from ES2015).

A value having the data type `Symbol` can be referred to as a symbol value. `Symbol` is an immutable primitive value that is unique. For example,

```jsx
// two symbols with the same description

const value1 = Symbol('hello');
const value2 = Symbol('hello');
```

## 2. Non-Primitive (Reference) Data Type

Non-primitive data types in JavaScript are not predefined. They are created by the programmer. Non-primitive data types are also called 'reference variables' or 'object references' as they reference a memory location where data is stored.

Below is a list of Non-Primitive Data Types with proper descriptions and examples:

### Object Data Type

An `object` is a complex data type that allows us to store collections of data. For example,

```jsx
const student = {
    firstName: 'hossain',
    lastName: null,
    class: 10
};
```

### Array Data Type

An `array` is an object that can store multiple values at once. For example,

```jsx
const words = ['hello', 'world', 'welcome'];
```

Here, `words` is an array. The array is storing 3 values.

### Regex Data Type

In JavaScript, a Regular Expression (RegEx) is an object that describes a sequence of characters used for defining a search pattern. For example,

```jsx
/^a...s$/
```

The above code defines a RegEx pattern. The pattern is: any five letter string starting with `a` and ending with `s`.

What's the difference between primitive vs reference in javascript?

[**Primitive vs. Reference**](Data%20Types%201b2aeacbb29981e8ab87e8748e4215f8/Primitive%20vs%20Reference%201b2aeacbb29981d2ac8cc6039c4a0d73.md)