# Operator Precedence

Operator precedence refers to the priority given to operators while parsing a statement that has more than one operator performing operations in it. Operators with higher priorities are resolved first. But as one goes down the list, the priority decreases and hence their resolution.

---

```jsx
( * ) and ( / ) have higher precedence than ( + ) and ( - )
```

## Precedence & Associativity

The associativity represents which operator has to solve first while going from left to right if two or more operators have the same precedence in the expression.

```jsx
2 + 3 * 4 / 3 =  2 + (3 * 4) / 3  // 6
```

The precedence of the multiply `( * )` and divide `( / )` operators is the same but due to associativity from left to right the multiply operator will be resolved first as it comes first when we go from left to right and hence the result will be 6.

## Operator Precedence & Associativity Table

The operator precedence and associativity table can help one know the precedence of an operator relative to other operators. As one goes down the table, the precedence of these operators decreases over each other. The operators as subparts of precedence will have the same specified precedence and associativity as contained by the main part.

### Expressions Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 18 | ( ) | Expression Grouping | (100 + 50) * 3 |
| 17 | . | Member Of | [person.name](http://person.name/) |
| 17 | [ ] | Member Of | person["name"] |
| 17 | ?. | Optional Chaining ES2020 | x ?. y |
| 17 | ( ) | Function Call | myFunction() |
| 17 | new | New with Arguments | new Date("June 5,2022") |
| 16 | new | New without Arguments | new Date() |
|  |  |  |  |

### Increment Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 15 | + + | Postfix Increment | i++ |
| 15 | - - | Postfix Decrement | i - - |
| 14 | + + | Prefix Increment | ++i |
| 14 | - - | Prefix Decrement | - - i |

### NOT Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 14 | ! | Logical NOT | ! ( x == y ) |
| 14 | ~ | Bitwise NOT | ~x |

### Unary Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 14 | + | Unary Plus | + x |
| 14 | - | Unary Minus | - x |
| 14 | typeof | Data Type | typeof x |
| 14 | void | Evaluate Void | void(0) |
| 14 | delete | Property Delete | delete myCar.color |

### Arithmetic Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 13 | ** | Exponentiation ES2016 | 10 ** 2 |
| 12 | * | Multiplication | 10 * 5 |
| 12 | / | Division | 10 / 5 |
| 12 | % | Division Remainder | 10 % 5 |
| 11 | + | Addition | 10 + 5 |
| 11 | - | Subtraction | 10 - 5 |
| 11 | + | Concatenation | "Hossain" + "Palin” |

### Shift Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 10 | << | Shift Left | x << 2 |
| 10 | >> | Shift Right (signed) | x >> 2 |
| 10 | >>> | Shift Right (unsigned) | x >>> 2 |

### Relational Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 9 | in | Property in Object | "PI" in Math |
| 9 | instanceof | Instance of Object | x instanceof Array |

### Comparison Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 9 | < | Less than | x < y |
| 9 | < = | Less than or equal | x <= y |
| 9 | > | Greater than | x > y |
| 9 | > = | Greater than or equal | x >= Array |
| 8 | == | Equal | x == y |
| 8 | === | Strict equal | x === y |
| 8 | ! = | Unequal | x != y |
| 8 | ! == | Strict unequal | x !== y |

### Bitwise Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 7 | & | Bitwise AND | x & y |
| 6 | ^ | Bitwise XOR | x ^ y |
| 5 | | | Bitwise OR | x | y |

### Logical Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 4 | && | Logical AND | x && y |
| 3 | | | | Logical OR | x || y |
| 3 | ?? | Nullish Coalescing ES2020 | x ?? y |

### Ternary Operator Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
| 2 | ? : | Condition | ? "yes" : "no” |

### Assignment Operators Precedence Values

| Value | Operator | Description | Example |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |