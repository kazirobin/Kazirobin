# Apply Method

**The `apply()` method calls a function with the passed this keyword value and arguments provided in the form of an array.**

```jsx
// object definition
const personName = {
  firstName: "Taylor",
  lastName: "Jackson",
};

// function definition
function greet(wish, message) {
  return `${this.firstName}, ${wish}. ${message}`;
}

// calling greet() function by passing two arguments
let result = greet.apply(personName, ["Good morning", "How are you?"]);

console.log(result);

// Output:
// Taylor, Good morning. How are you?
```

## Apply Syntax

The syntax of the `apply()` method is:

```jsx
func.apply(thisArg, argsArray)
```

Here, `func` is a function.

## Apply Parameters

The `apply()` method can take **two** parameters:

- `thisArg` - The value of `this` which is provided while calling `func`.
- `argsArray` (optional) - An array containing the arguments to the function.

## Apply Return Value

Returns the result of the called function with the specified `this` value and arguments.

## Apply Method to call a Function

```jsx
// object definition
const personName = {
  firstName: "Taylor",
  lastName: "Jackson",
};

// function definition
function greet(wish, message) {
  return `${this.firstName}, ${wish}. ${message}`;
}

// calling greet() function by passing two arguments
let result = greet.apply(personName, ["Good morning", "How are you?"]);

console.log(result);
```

### Output

```jsx
Taylor, Good morning. How are you?
```

In the above program, we have used the `apply()` method to invoke the `greet()` function.
Inside the `apply()` method, the parameter:

- personName - is `this` value
- `["Good morning", "How are you?"]` - are values for `"wish"` and `"message"` parameters of the `greet()` function

The method calls the `greet()` function so the result variable holds the return value of `greet()`.

Apart from calling a function, we can use the `apply()` method for:

- Function borrowing
- Append an array

## Apply for Function Borrowing

```jsx
// object definition
const car = {
  name: "BMW",
  description() {
    return `The ${this.name} is of ${this.color} color.`;
  },
};

// object definition
const bike = {
  name: "Duke",
  color: "black",
};

// bike is borrowing description() method from car using apply() 
let result = car.description.apply(bike);

console.log(result);
```

### Output

```jsx
The Duke is of black color.
```

In the above program, we have borrowed the method of `car` object in the `bike` object with the help of the `apply()` method.

## Apply to Append two Arrays

```jsx
let color1 = ["Red", "Green", "Blue"];
let color2 = ["Yellow", "Black"];

// appending two arrays color1 and color2
color1.push.apply(color1, color2);

console.log(color1);
```

### Output

```jsx
[ 'Red', 'Green', 'Blue', 'Yellow', 'Black' ]
```

## Using Apply with built-in functions

```jsx
const numbers = [5, 1, 4, 3, 4, 6, 8];

// using apply() with Math object
let max = Math.max.apply(null, numbers);

console.log(max);

// without using apply() with Math object
let max1 = Math.max(5, 1, 4, 3, 4, 6, 8);

console.log(max1);
```

### Output

```jsx
8
8
```