# Mongoose Schema

Mongoose schemas are how you tell Mongoose what your documents look like. Mongoose schemas are separate from TypeScript interfaces, so you need to either define both a raw document interface and a schema; or rely on Mongoose to automatically infer the type from the schema definition.

---

## Create Mongoose Schema Model

*Models* are higher-order constructors that take a schema and create an instance of a document equivalent to records in a relational database.

## Schema Types

While Mongoose schemas define the overall structure or shape of a document, *SchemaTypes* define the expected data type for individual fields (`String`, `Number`, `Boolean`, and so on).

You can also pass in useful options like `required` to make a field non-optional, `default` to set a default value for the field, and many more.

Create a file named **src/models/user-model.js**

```jsx
import { Schema, model, models } from 'mongoose';

const UserSchema = new Schema({
  name: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  phone: {
    type: String,
  },
});

export const Users = models.users || model('users', UserSchema);
```

```jsx
import { Schema, model, models } from 'mongoose';

const UsersSchema = new Schema(
  {
    name: {
      type: String,
      default: 'Anonymous',
      min: 2,
      max: 100,
      required: [true, 'Name must be provided'],
    },
    email: {
      type: String,
      match: /.+\@.+\..+/,
      unique: true,
      min: 2,
      max: 100,
      required: [true, 'Email must be provided'],
    },
    password: {
      type: String,
      min: 5,
      required: [true, 'Password must be provided'],
    },
    uid: {
      type: String,
      unique: true,
    },
    roles: {
      type: [Number],
      default: [2001],
    },
    is_admin: {
      type: Boolean,
      default: false,
    },
    active: {
      type: Boolean,
      default: true,
    },
    softDelete: {
      type: Boolean,
      default: false,
    },
    lastLoginAt: {
      type: String,
      default: Date.now(),
    },
    refreshToken: {
      type: String,
      default: null,
    },
    sAccessToken: {
      type: String,
      default: null,
    },
    issuedAt: {
      type: Number,
      default: 101010,
    },
    occupation: String,
    deletedAt: String,
    provider: String,
    image: String,
    bio: String,
    lastLoginIp: String,
    city: String,
    state: String,
    country: String,
    phoneNumber: String,
    forgotPasswordToken: String,
    forgotPasswordTokenExpiry: Date,
    verifyToken: String,
    verifyTokenExpiry: Date,
  },
  { timestamps: true },
);

export const Users = models.users || model('users', UsersSchema);
```