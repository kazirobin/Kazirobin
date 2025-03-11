# Object.create()

This is the easiest way to link an object to a prototype object. It is a method used to create a new object with the specified prototype object and properties.

The object.create() method returns a new object with the specified prototype object and properties.

```jsx
const User = {
    init(name){
        this.name = name
    },

    printName(){
        console.log(this.name);
    }
}

let kedar = Object.create(User)
kedar.init("kedar")
kedar.printName()
```

The newly created object will inherit all the prototype object's properties. You can specify a second parameter to add new properties to the object, that the prototype lacked:

```jsx
const newObject = Object.create(prototype, newProperties)
```

```jsx
const User = {

    printName(){
        console.log(this.name);
    }
}

let properties = {
    name: {
        value:"John"
    }

}

let John = Object.create(User,properties)
John.printName()
```

## How Does Inheritance Work?

Implementing inheritance in Object.create() is simple. Check out the code below:

```jsx
const User = {
    printName(){
        console.log(this.name);
    },

    init(name, password){
        this.name = name
        this.password = password
    }
}

const Admin = Object.create(User)
Admin.init = function(name, password, course){
    User.init.call(this, name, password)
    this.course = course
}

Admin.stats = function(){
    console.log("Stats");
}

const kedar = Object.create(Admin)
kedar.init("kedar", 123456)
kedar.printName()
kedar.stats()
```

### Output

![ss9-1.png](Object%20create()%201b2aeacbb29981e18f58c994eaa0694c/ss9-1.png)

First, we created a User function. Then we created an Admin pointing to User with the help of `Object.create()`. With the help of the `Admin.init()` method we called the `init()` method of User and passed values to the parent function.