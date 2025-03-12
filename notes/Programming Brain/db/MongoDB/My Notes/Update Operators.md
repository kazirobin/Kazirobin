# Update Operators

MongoDB provides several **update operators** that allow you to modify the values of fields in a document. These operators can be used in `update`, `updateOne`, `updateMany`, and `findAndUpdate` queries.

## `$set`

The `$set` operator is used to update a field with a new value. If the field doesn't exist, it will be created.

```jsx
db.users.updateOne(
  { name: "John" },
  { $set: { age: 30 } }
);
```

This updates the `age` field of the user named "John" to `30`.

## `$unset`

The `$unset` operator is used to remove a field from a document.

```jsx
db.users.updateOne(
  { name: "John" },
  { $unset: { age: "" } }
);
```

This removes the `age` field from the document of the user named "John".

## `$inc`

The `$inc` operator increments (or decrements) the value of a field by a specified amount. If the field does not exist, it will be created and set to the increment value.

```jsx
db.users.updateOne(
  { name: "John" },
  { $inc: { age: 1 } }
);
```

This increments the `age` field of the user named "John" by 1.

## `$mul`

The `$mul` operator multiplies the value of a field by a specified value.

```jsx
db.users.updateOne(
  { name: "John" },
  { $mul: { age: 2 } }
);
```

This multiplies the `age` field of the user named "John" by `2`.

## `$rename`

The `$rename` operator renames a field in a document.

```jsx
db.users.updateOne(
  { name: "John" },
  { $rename: { "age": "years" } }
);
```

This renames the `age` field to `years` for the user named "John".

## `$push`

The `$push` operator appends a value to an array. If the field does not exist, it will be created as an array.

```jsx
db.users.updateOne(
  { name: "John" },
  { $push: { hobbies: "reading" } }
);
```

This adds `"reading"` to the `hobbies` array of the user named "John".

## `$push` with `$each`

The `$push` operator can also be used with `$each` to add multiple values at once to an array.

```jsx
db.users.updateOne(
  { name: "John" },
  { $push: { hobbies: { $each: ["reading", "traveling"] } } }
);
```

This adds both `"reading"` and `"traveling"` to the `hobbies` array of the user named "John".

## `$addToSet`

The `$addToSet` operator adds a value to an array only if the value does not already exist. It ensures unique values in the array.

```jsx
db.users.updateOne(
  { name: "John" },
  { $addToSet: { hobbies: "reading" } }
);
```

This adds `"reading"` to the `hobbies` array of the user named "John" only if it is not already present.

## `$pop`

The `$pop` operator removes the first or last element from an array.

- Use `1` to remove the last element.
- Use `-1` to remove the first element.

```jsx
db.users.updateOne(
  { name: "John" },
  { $pop: { hobbies: 1 } }
);
```

This removes the last element from the `hobbies` array of the user named "John".

## `$pull`

The `$pull` operator removes all instances of a value from an array that match a specified condition.

```jsx
db.users.updateOne(
  { name: "John" },
  { $pull: { hobbies: "reading" } }
);
```

This removes `"reading"` from the `hobbies` array of the user named "John".

## `$pullAll`

The `$pullAll` operator removes all instances of any value in the array that matches any of the specified values.

```jsx
db.users.updateOne(
  { name: "John" },
  { $pullAll: { hobbies: ["reading", "traveling"] } }
);
```

This removes both `"reading"` and `"traveling"` from the `hobbies` array of the user named "John".

## `$slice`

The `$slice` operator limits the number of elements in an array that are returned in an update.

```jsx
db.users.updateOne(
  { name: "John" },
  { $slice: { hobbies: -2 } }
);
```

This keeps the last two elements in the `hobbies` array.

## `$setOnInsert`

The `$setOnInsert` operator is used with the `upsert` option. It sets the value of a field only when a new document is inserted (i.e., when no matching document is found).

```jsx
db.users.updateOne(
  { name: "John" },
  { $setOnInsert: { age: 30 } },
  { upsert: true }
);
```

This sets the `age` field to `30` only if no document matching the name "John" is found.

## `$currentDate`

The `$currentDate` operator sets a field to the current date. It can set the field to either the **current date** or the **current timestamp**.

- Use `true` for a date.
- Use `{ $type: "timestamp" }` for a timestamp.

```jsx
db.users.updateOne(
  { name: "John" },
  { $currentDate: { lastModified: true } }
);
```

This sets the `lastModified` field to the current date for the user named "John".

## `$bit`

The `$bit` operator performs bitwise operations on an integer field.

```jsx
db.users.updateOne(
  { name: "John" },
  { $bit: { flags: { and: 2 } } }
);
```

This performs a bitwise `AND` operation on the `flags` field with `2`.

## `$merge`

The `$merge` operator allows you to merge the results of an aggregation pipeline into a collection. It's used for advanced update scenarios.

```jsx
db.orders.aggregate([
  { $match: { status: "pending" } },
  { $merge: { into: "archived_orders" } }
]);
```

This merges documents from the `orders` collection with `status` set to `"pending"` into the `archived_orders` collection.