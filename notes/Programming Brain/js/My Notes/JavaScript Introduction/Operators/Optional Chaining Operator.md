# Optional Chaining Operator

The optional chaining operator (`?.`) is like a shortcut for accessing nested properties in a series of objects. Instead of having to check if each step in the chain is empty (`null` or `undefined`), you can use the operator `?.` to directly access the desired property.

If any part of the chain is empty, the optional chaining operator (`?.`) will stop right there and give you `undefined` as a result. It saves you from writing extra checks for each step in the chain.

Suppose that you have a function that returns a `user` object:

```jsx
function getUser(id) {

    if(id <= 0) {
        return null;
    }

    // get the user from database
    // and return null if id does not exist
    // ...
    
    // if user was found, return the user
    return {
        id: id,
        username: 'admin',
        profile: {
            avatar: '/avatar.png',
            language: 'English'
        }
    }
}
```

The following uses the `getUser()` function to access the user profile:

```jsx
let user = getUser(1);
let profile = user.profile;
```

However, if you pass the `id` that is less than or equal to zero or the `id` doesn’t exist in the database, the `getUser()` function will return `null`.

In this example, we confirm that the `user` is not `null` or `undefined` before accessing the value of `user.profile` property. It prevents the error that would occur if you simply access the `user.profile` directly without checking the user first.

ES2020 introduced the optional chaining operator denoted by the question mark followed by a dot:

```jsx
?.
```

To access a property of an object using the optional chaining operator, you use one of the following:

```jsx
objectName ?. propertyName // optional static property access
objectName ?. [expression] // optional dynamic property access
```

The optional chaining operator implicitly checks if the `user` is not `null` or `undefined` before attempting to access the `user.profile`:

```jsx
let user = getUser(2);
let profile = user ?. profile;
```

In this example, if the `user` is `null` or `undefined`, the optional chaining operator (`?.`) immediately returns `undefined`.

Technically, it is equivalent to the following:

```jsx
let user = getUser(2);
let profile = (user !== null || user !== undefined) ? user.profile : undefined;
```