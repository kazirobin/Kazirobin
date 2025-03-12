# ES6 Classes

Classes are an alternative to the constructor function syntax for implementing prototypal inheritance. We also call classes `syntactic sugar`.

Behind the scenes, classes work exactly like constructor functions. Prior to ES6, JavaScript had no concepts of classes. To mock a class, you often use the [constructor or prototype pattern](https://www.javascripttutorial.net/javascript-constructor-prototype/).

We can implement OOP using classes, but behind the scenes it uses prototypal inheritance. This method was introduced to make sense to people coming from other languages like C++ and Java.

We will implement the User classes from the above example:

```jsx
// Class Expression
class User = class{

}

// Class Declaration
class User{

}
```

In the above example, we can see that there are 2 ways to implement a class in JavaScript. You can choose either one according to your preference.

Inside the class, the first thing we need to do is add a constructor method. The constructor can also take arguments.

```jsx
class User {
    constructor(name) {
        this.name = name
    }

    printName() {
        console.log(this.name);
    }
}

const kedar = new User("kedar")
```

### Output

![ss7-1.png](ES6%20Classes%201b2aeacbb29981ba88f2f099480d6d9d/ss7-1.png)

Remember that whenever we create an object of a class, a constructor is invoked first. If there is no constructor, the default constructor is invoked which does nothing.

## 3 things to remember about classes

- Classes are not hoisted.
- Classes are first-class citizens.
- Classes are executed in strict mode.

## What are Setters and Getters?

These are simple methods of classes which will get and set a value. But from the outside they look like simple methods. Let's take a look at the below example.

```jsx
class User{
    constructor(name){
        this._name = name
    }

    get getName(){
        console.log(this._name)
    }

    set setName(newName){
        this._name = newName
    }
}

const kedar = new User("kedar")
kedar.setName = "John"
kedar.getName
```

In above example, you can see the getter `getName` logs a name. Setters are used to set the value of an existing property. When setting a name using setter, we have to use (_) before the name of the property as a convention.

## How to Use Static Methods

Static methods are bound to a class and not to the instances of class or object of the class. We can access static methods through classes only and not through the object of that class.

```jsx
class User{
    constructor(name){
        this._name = name
    }

    static anonymous(){
        console.log("anonymous");
    }
}

const kedar = new User("kedar")
kedar.anonymous() // error
User.anonymous() // "anonymous"
```

We can directly create static methods inside classes using the `static` keyword before the method name. In the above example, notice that we can only call the static method on a class and not on a class object.

**There is one more way to implement a static method:**

```jsx
class User{
    constructor(name){
        this._name = name
    }
}

User.anonymous = function(){
    console.log("anonymous");
}

const kedar = new User("kedar")
kedar.anonymous() // error
User.anonymous() // "anonymous"
```

## How Does Inheritance Work?

It is super simple to implement inheritance using ES6 syntax. But remember ES6 uses constructor functions to implement inheritance behind the scenes.

```jsx
class User{
    constructor(name, password){
        this.name = name
        this.password  =password
    }

    printName(){
        console.log(this.name);
    }
}

class Admin extends User{
    constructor(name, password, course){
        super(name, password)
        this.course = course
    }

    Stats(){
        console.log("Stats");
    }
}

const kedar = new Admin("kedar", 123456, "JavaScript")
kedar.printName()
```

So we have 2 classes, User and Admin. When we want to inherit, we simply add `extends` and the class we want to inherit from in-front of the child class similar to the syntax shown in the above code.

When we are done with that, in the constructor of the child class, we call the `super()` method to pass an argument to the parent class which is required. That's how we can implement inheritance in JavaScript using ES6 syntax.

We can also **`override` the** parent method by implementing a method with the same name in the child class.

```jsx
class User{
    constructor(name, password){
        this.name = name
        this.password  =password
    }

    printName(){
        console.log(this.name);
    }
}

class Admin extends User{
    constructor(name, password, course){
        super(name, password)
        this.course = course
    }

    Stats(){
        console.log("Stats");
    }

    printName(){
        console.log("Child class " + this.name)
    }
}

const kedar = new Admin("kedar", 123456, "JavaScript")
kedar.printName()
```