# GraphQL Type System

The **GraphQL** type system is a fundamental concept in GraphQL that defines the structure and **capabilities** of a GraphQL server. It plays an important role in specifying the data types used in a GraphQL application and helps define the schema, which acts as a contract between the **client** and the **server**.

## What is a GraphQL Type System?

- GraphQL is a **strongly typed language**, which means **every piece of data in a GraphQL service has a specific type.**
- It is a concept in **GraphQL** which is used to describe the potential of a GraphQL server.
- It helps to define the various data types which are used in a GraphQL application. With the help of Type System, it helps to define the schema, which is a contract between the **client** and the **server**.
- It tells us what data type can be queried and what are the operations which can be performed. It also informs us whether a query is **valid or not.**
- The type system also ensures that queries are valid and provides a clear structure for interacting with the server.

## Different Types of Type System

### 1. Scalar Type

- These types are **primitive** data types. These data types tend to store only a single value.GraphQL offers various default scalar types:
- **Int:** Signed 32-bit Integer.
- **Float:** Signed number with values in integer and decimal form.
- **String:** UTF - 8-character sequence.
- **Boolean:** True or false.
- **ID:** It is a unique identifier that is particularly used for identifying an item or object.

**Syntax:**

```
scalar Int
scalar Float
scalar String
scalar Boolean
scalar ID
```

**Example:**

Suppose we have a schema for a blog application, and we want to define a Post type that includes a title and content, both of which are strings.

```
type Post {
  id: ID!
  title: String!
  content: String!
  createdAt: DateTime!
}
```

### 2. Object Type

- It is regarded as the most common type of data type which is used in a schema.
- It allow users to represent a group of fields as a whole.It also supports the nested type features in this data type.

**Syntax:**

```
type Employee {
  id: Int!
  name: String!
  age: Int!
  address: Address!
}
```

**Example:**

Suppose we want to store the basic structure for storing employee information in a GraphQL schema.

```
type Employee {  
   id: Int!
   firstname: String!
   age: Int!
   salary: Float!
}
```

**GraphQL schema**

```
type Query {  
   getEmployees: [Employee] 
}
```

### 3. Query Type

- These data types are used to define the entry points for retrieving the data.
- It is among the top root-level types in GraphQL. Basically it is a request which is sent from the client to the server.

**Syntax:**

```
type Query {   
	getEmployeeById(id: Int!): Employee
}
```

**Example:**

Suppose we want to greet message from the server in a GraphQL query.

```
type Query  {
   greeting: String
}
```

### 4. Mutation Type

- The Mutation Type is among the top root-level types in GraphQL.
- It is used to specify the entry point to perform the data mainpulations operations. It performs operations like create, update or delete data.

**Syntax:**

```
type Mutation {   
	createEmployee(name: String!, age: Int!): Employee!
	updateEmployee(id: Int!, name: String, age: Int): Employee
	deleteEmployee(id: ID!): Boolean
}
```

**Example:**

Suppose we want to add a new employee to the system.

```
type Mutation {  
   addEmployee(firstName: String, lastName: String): Employee  
}
```

### 5. Enum Type

- This data type is used to represent the leaf values in a GraphQL type system.
- This data types is preferred to use where the user have a list of options to choose from. It is very much similar to the scalar type.

**Syntax**:

```
type enum_name{
val_1
val_2
}
```

**Example:**

```
type Days_of_Week{  
   SUNDAY  
   MONDAY  
   TUESDAY  
   WEDNESDAY  
   THURSDAY  
   FRIDAY  
   SATURDAY  
}
```

### 6. List Type

- This data type is used to represent a collection.
- It is generally used to represent an array of values of a particular type.It is used with the type modifier to wraps similar obhects, scalar, enum etc.

**Syntax:**

```
field:[data_type]
```

**Example:**

Suppose we want to returns a list of strings, representing a to-do list.

```
type Query {  
   todo: [String]  
}
```

### 7. Non-Nullable Type

- This data type has a special feature or characteristics through which it can either return a value of the specified type or it can have no value.
- To define a non-nullable type, the field must be defined with an exclamation mark`(!)`**.**

**Syntax:**

```
field:data_type!
```

**Example**:

Suppose we want to define the field for the employee where the employee if can't be NULL.

```
type Employee {  
   id:ID! 
   firstName:String
   lastName:String
}
```