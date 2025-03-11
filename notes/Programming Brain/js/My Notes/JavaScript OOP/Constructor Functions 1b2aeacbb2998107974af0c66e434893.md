# Constructor Functions

We can create objects from a function. With the help of a constructor function, built-in objects like arrays, sets, and others are actually implemented.

In JavaScript, a constructor gets called when an object is created using the `new` keyword. The purpose of a constructor is to create a new object and set its values for any existing object properties

We will use a function to create prototypal inheritance. We will start by implementing a User function expression. Remember to always start the name of a constructor function with capital letter (standard convention).

```jsx
function User(name){
    this.name = name;

    // never create function inside constructor function
    this.printName = function(){
        console.log(this.name);
    }

    console.log(this);
}

let kedar = new User("kedar")
```

### Output

![ss2-2.png](Constructor%20Functions%201b2aeacbb2998107974af0c66e434893/ss2-2.png)

We created a constructor function in the above example. But what is the `new` keyword? With the help of the new keyword we can create an instance of that constructor.

When we create an instance of the constructor object, an empty object is created ({}). This empty object ({}) is then linked to the prototype.

We should never create a function inside of a constructor function. Because every time an instance is created, a new function is created with it which we created inside the constructor function. This will create major issues for performance.

The solution to this problem is prototypes. We can define a function on the prototype of an object directly. So the object created by using that constructor function will have access to that function.

### Example

```jsx
function User(name){
    this.name = name;

    console.log(this);
}

User.prototype.printName = function(){
    console.log(this.name)
}

let kedar = new User("kedar")
```

### Output

![ss3-2.png](Constructor%20Functions%201b2aeacbb2998107974af0c66e434893/ss3-2.png)

In the above output, you can see the `printName()` method in the prototype of the User constructor function. This is the preferred way to create a function in a constructor function to optimize performance.

So now all objects created by this constructor function will have access to the printName() function.

We can access these functions with objectName.functionName() like this:

```jsx
function User(name){
    this.name = name;

    console.log(this);
}

User.prototype.printName = function(){
    console.log(this.name)
}

let kedar = new User("kedar")
kedar.printName()
```

We can access the prototype of the constructor function with the following syntax:

```jsx
console.log(User.__proto__)
```

The object prototype is the same as the constructor function prototype. Don't believe me? Check this out:

```jsx
console.log(kedar.__proto__ === User.prototype) 
// True

console.log(User.prototype.isPrototypeOf(kedar))
// True
```

The prototype of User is the prototype used by its object and doesn't belong to User.

```jsx
console.log(User.prototype.isPrototypeOf(User))
// False
```

We can also link a variable to prototype:

```jsx
User.prototype.species = "Hossain M Pain"
```

## Prototypal Inheritance of Built-in Objects

We have many methods available to use on arrays. How does this work?

The answer is prototypal inheritance. When we create a new array, every time it inherits from Array.prototype. That is how we have access to all those different methods.

```jsx
const arr = [1,2,3,4,5]
console.log(arr)
```

![ss5-2.png](Constructor%20Functions%201b2aeacbb2998107974af0c66e434893/ss5-2.png)

We can also attach our own method to Array.prototype so that whenever we create new array we will have access to that method.

```jsx
const arr = [1,2,4,4,5,5]

Array.prototype.unique = function(){
    return [...new Set(this)]
}

console.log(arr.unique());
```

![ss6-2.png](Constructor%20Functions%201b2aeacbb2998107974af0c66e434893/ss6-2.png)

## How Does Inheritance Work?

Let's understand constructor function inheritance by example.

```jsx
const User = function(name, password){
    this.name = name
    this.password = password
}

User.prototype.printName = function(){
    console.log(this.name);
}

const Admin = function(name, password){
    this.name = name
    this.password = password
}

Admin.prototype.Stats = function(){
    console.log("Stats");
}

const kedar = new Admin("kedar", 12345)
kedar.Stats()
```

In the above code, we have 2 constructor functions, and they have some similarities. Still we wrote it twice which violates the DRY (Don't Repeat Yourself) principle. To avoid repeating the same code, we use inheritance.

```jsx
const User = function(name, password){

    this.name = name
    this.password = password
}

User.prototype.printName = function(){
    console.log(this.name);
}

const Admin = function(name, password, course){
    User.call(this, name, password)
    this.course = course
}

Admin.prototype = Object.create(User.prototype)

Admin.prototype.Stats = function(){
    console.log("Stats");
}

const kedar = new Admin("kedar", 12345, "JavaScript")
kedar.printName()
```

In the above code, first in the Admin (child) function we attached `this` to the User (parent) and called it with parameters. Once we did that, we were able to access the name and password fields. But we were not able to access the methods of the parent function. Because we need to connect the prototype of User and Admin.

For that, just after the child function, we pointed the Admin prototype to the User prototype which gave us access to the methods of the parent function (User).

Make sure to point the child (Admin) prototype to the parent (User) function immediately after the child (Admin) function. Because it returns an empty object and removes all methods on the child (Admin) function. So always create methods of the child (Admin) function after pointing the child (Admin) prototype to the parent (User) prototype.

Now let's see how our prototype chain looks:

![ss8-1.png](Constructor%20Functions%201b2aeacbb2998107974af0c66e434893/ss8-1.png)

At the bottom there is an Object prototype. After that we can see there is a User prototype and at the top we see an Admin prototype.