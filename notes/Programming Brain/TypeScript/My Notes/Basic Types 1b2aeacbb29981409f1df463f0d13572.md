# Basic Types

For programs to be useful, we need to be able to work with some of the simplest units of data: numbers, strings, structures, boolean values, and the like. In TypeScript, we support the same types as you would expect in JavaScript, with an extra enumeration type thrown in to help things along.

## Primitive Types

These are the most basic types in TypeScript.

- `string`

```tsx
let name: string = "Hussain";
```

- `number`

```tsx
let age: number = 25;
```

- `boolean`

```tsx
let isDeveloper: boolean = true;
```

- `null`

```tsx
let emptyValue: null = null;
```

- `undefined`

```tsx
let notAssigned: undefined = undefined;
```

- `bigint`

```tsx
let bigNumber: bigint = 9007199254740991n;
```

- `symbol`

```tsx
let uniqueId: symbol = Symbol("id");
```

## Any Type

Allows any type of value, but removes type safety.

```tsx
let anything: any = "Hello";
anything = 42; // No error
```

## Unknown Type

Similar to `any`, but requires type checking before usage.

```tsx
let unknownVar: unknown = "Hello";

if (typeof unknownVar === "string") {
  console.log(unknownVar.toUpperCase());
}
```

## Void Type

Used when a function does not return anything.

```tsx
function logMessage(): void {
  console.log("This function returns nothing.");
}
```

## Never Type

Used when a function never returns (e.g., errors or infinite loops).

```tsx
function throwError(message: string): never {
  throw new Error(message);
}
```

## Object Type

Used for objects with specific key-value pairs.

```tsx
let user: { name: string; age: number } = {
  name: "Hussain",
  age: 25,
};
```

## Array Types

- Simple Array

```tsx
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["Alice", "Bob"];
```

- Tuple (Fixed-Length Array)

```tsx
let userTuple: [string, number] = ["Hussain", 25];
```

## Union Type

Allows multiple possible types.

```tsx
let id: string | number;
id = "123"; // OK
id = 123;   // OK
```

## Intersection Type

Combines multiple types into one.

```tsx
type Person = { name: string };
type Employee = { id: number };

let worker: Person & Employee = { name: "Hussain", id: 101 };
```

## Type Alias

A custom name for a type.

```tsx
type ID = number;
let userId: ID = 123;
```

## Literal Type

Specifies exact values a variable can hold.

```tsx
let direction: "up" | "down";
direction = "up"; // OK
// direction = "left"; // Error
```

## Enum Type

Defines a set of named constants.

```tsx
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE",
}

let selectedColor: Color = Color.Red;
console.log(selectedColor); // Output: "RED"
```

## Function Type

Defines the type of a function.

```tsx
let add: (a: number, b: number) => number;
add = (a, b) => a + b;
```

## Interface

Defines a blueprint for objects.

```tsx
interface Person {
  name: string;
  age: number;
}

let userObj: Person = { name: "Hussain", age: 25 };
```

## Class Types

```tsx
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, my name is ${this.name}`;
  }
}

let person1 = new Person("Hussain", 25);
console.log(person1.greet());
```

## Mapped Types

Used to create new types from existing ones. `OptionalUser` is a new type where each property of `User` is made optional. The `keyof` operator retrieves all keys from `User`, and the `mapped` type iterates over each key, marking them as optional with `?`.

```tsx
type User = { name: string; age: number };
type OptionalUser = { [K in keyof User]?: User[K] };

let newUser: OptionalUser = { name: "Hussain" };
```

## Conditional Types

Used to create types based on conditions.

```tsx
type IsString<T> = T extends string ? "Yes" : "No";

type Test1 = IsString<string>; // "Yes"
type Test2 = IsString<number>; // "No"
```

## Readonly and Partial Types

- Readonly

Prevents modifica

```tsx
type User = { readonly id: number; name: string };

let user: User = { id: 1, name: "Hussain" };
// user.id = 2; // Error
```

- Partial

Makes all properties optional.

```tsx
type User = { id: number; name: string };
type PartialUser = Partial<User>;

let user2: PartialUser = { name: "Hussain" };
```

## Record Type

Creates an object type with specific key-value pairs.

```tsx
type Users = Record<string, number>;
let users: Users = { Hussain: 25, Alice: 30 };
```

## Pick and Omit Types

- **Pick** (Selects specific properties)

```tsx
type Person = { name: string; age: number; location: string };
type NameAndAge = Pick<Person, "name" | "age">;

let user: NameAndAge = { name: "Hussain", age: 25 };
```

- **Omit** (Excludes specific properties)

```tsx
type WithoutLocation = Omit<Person, "location">;
```

## Utility Types

TypeScript provides built-in utility types like:

- `Required<T>`: Makes all properties required.
- `Partial<T>`: Makes all properties optional.
- `Readonly<T>`: Makes properties read-only.
- `Record<K, T>`: Creates an object type.

```tsx
type User = { name: string; age?: number };
type RequiredUser = Required<User>; // { name: string; age: number }
```

## Generic Type

A **generic type** in TypeScript is a way to create `reusable` ****and `flexible` components by allowing types to be **dynamically defined**. Instead of specifying a fixed type, generics use a **placeholder (like `T`)**, which can be replaced with an actual type when used.

### Why Use Generics?

- `Reusability` – Write code that works with multiple types.
- `Type Safety` – Helps catch type-related errors at compile time.
- `Flexibility` – Allows functions, classes, and interfaces to work with any type.

### 1. Generic Functions

The `<T>` means **"this function will accept and return the same type"**. TypeScript **infers** `T` from the passed argument.

```tsx
function identity<T>(value: T): T {
  return value;
}

let str = identity<string>("Hello");
console.log(str.toUpperCase()); // ✅ Safe, TypeScript knows str is a string
```

Even better, TypeScript can infer the type automatically:

```tsx
let num = identity(100); // TypeScript infers T as number
console.log(num.toFixed(2)); // ✅ Safe
```

### 2. Generic Interfaces

Generics allow interfaces to work with multiple types.

```tsx
interface Box<T> {
  content: T;
}

let stringBox: Box<string> = { content: "Hello" };
let numberBox: Box<number> = { content: 42 };

console.log(stringBox.content.toUpperCase()); // ✅ Works
console.log(numberBox.content.toFixed(2));    // ✅ Works
```

`T` is **replaced** with `string` or `number`, depending on usage.

### 3. Generic Classes

Classes can also be generic, making them more flexible.

```tsx
class Storage<T> {
  private items: T[] = [];

  addItem(item: T): void {
    this.items.push(item);
  }

  getItems(): T[] {
    return this.items;
  }
}

let stringStorage = new Storage<string>();
stringStorage.addItem("Apple");
console.log(stringStorage.getItems()); // ✅ ['Apple']

let numberStorage = new Storage<number>();
numberStorage.addItem(10);
console.log(numberStorage.getItems()); // ✅ [10]
```

- `Storage<T>` can store **any type** (`string`, `number`, etc.).
- The type is **set when creating an instance**.

### 4. Generic Constraints

You can **restrict** what types are allowed in a generic.

```tsx
function printLength<T extends { length: number }>(value: T): void {
  console.log(value.length);
}

printLength("Hello");    // ✅ Works (string has a length)
printLength([1, 2, 3]);  // ✅ Works (array has a length)
// printLength(100);     // ❌ Error: number doesn't have a length property
```

`T extends { length: number }` ensures that only **objects with a `length` property** can be used.

### 5. Generic Type Aliases

You can use generics with `type`.

```tsx
type Pair<T, U> = { first: T; second: U };

let person: Pair<string, number> = { first: "Hussain", second: 25 };
```

The type alias `Pair<T, U>` allows **two generic types**.

### 6. Default Generic Type

You can provide **default values** for generics.

```tsx
type Response<T = string> = { data: T };

let response1: Response = { data: "Success" };  // Defaults to string
let response2: Response<number> = { data: 200 }; // Explicitly number
```

If **no type** is provided, it **defaults to `string`**.