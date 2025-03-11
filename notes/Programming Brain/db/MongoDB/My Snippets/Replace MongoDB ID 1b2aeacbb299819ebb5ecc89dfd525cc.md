# Replace MongoDB ID

Replace all instances of ***_id to id*** in your codebase. And create a new field when exporting the collection

```jsx
// Replace mongo db _id in object
export const replaceMongoIdInObject = (obj: any) => {
  if (!obj || typeof obj !== "object") return obj;

  if (obj.toObject) {
    obj = obj.toObject();
  }

  const { _id, ...rest } = obj;
  return { id: _id?.toString(), ...rest };
};

// Replace mongo db _id in array
export const replaceMongoIdInArray = (array: any) => {
  return array.map((obj: any) => replaceMongoIdInObject(obj));
};
```