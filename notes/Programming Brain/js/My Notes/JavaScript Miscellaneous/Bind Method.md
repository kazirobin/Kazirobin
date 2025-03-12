# Bind Method

**The `bind()` method allows an object to borrow a method from another object without copying.**

```jsx
// object definition
const student1 = {
  name: "Jack",
  grade: "5",
  introduction: function () {
    console.log(this.name + "studies in grade" + this.grade + ".");
  },
};

// object definition
const student2 = {
  name: "Jimmy ",
  grade: " 6",
};

// the object student2 is borrowing introduction method from student1
let result= student1.introduction.bind(student2);

// invoking introduction() function
result();

// Output:
// Jimmy studies in grade 6.
```

## Bind Syntax

The syntax of the `bind()` method is:

```jsx
func.bind(thisArg, arg1, ... argN)
```

Here, `func` is a function.

## Bind Parameters

The `bind()` can take **two** parameters:

- `thisArg` - The value provided as this parameter for `func`.
- `arg1, ... argN` (optional) - The value of arguments present inside `func`.

**Note:** If `thisArg` is not specified, the this of the executing scope is treated as `thisArg`.

## Bind Return Value

Returns a copy of the given function with the specified `this` value, and initial arguments (if provided).

## Using Bind Method

```jsx
// object definition
const student1 = {
  name: "Jack",
  grade: "5",
  introduction: function () {
    console.log(this.name + "studies in grade" + this.grade + ".");
  },
};

// object definition
const student2 = {
  name: "Jimmy ",
  grade: " 6",
};

// the object student2 is borrowing introduction method from student1
let result= student1.introduction.bind(student2);

// invoking result() function
result();  // Jimmy studies in grade 6.
```

### Output

```jsx
Jimmy studies in grade 6.
```

In the above example, we have defined two objects student1 and student2.

Since student2 doesn't have the `introduction()` method, we are borrowing it from student1 using the `bind()` function.

`student1.introduction.bind(student2)` returns the copy of `introduction()` and assigns it to result.

## Using Bind Method with two Parameters

```jsx
// object definition
const student1 = {
  name: "Jack",
  introduction: function (score) {
    console.log(this.name + "scored " + score + " in an exam.");
  },
};

// object definition
const student2 = {
  name: "Jimmy ",
};

// passing two parameters student2 and '95'
let result = student1.introduction.bind(student2, 95);

// invoking result() function
result(); // Jimmy scored 95 in an exam.
```

### Output

```jsx
Jimmy scored 95 in an exam.
```

In the above example, we have passed two parameters thisArg and `arg1` in `bind()`.

The student2 object is passed as `this` parameter and **95** is passed as an argument for the score parameter.