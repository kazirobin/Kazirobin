# Regex

In JavaScript, a **Reg**ular **Ex**pression (RegEx) is an object that describes a sequence of characters used for defining a search pattern. For example,

```jsx
/^a...s$/
```

The above code defines a RegEx pattern. The pattern is: **any five letter string starting with** `a` **and ending with** `s`.

A pattern defined using RegEx can be used to match against a string.

| Expression | String | Matched? |
| --- | --- | --- |
| `/^a...s$/` | `abs` | No match |
| `/^a...s$/` | `alias` | Match |
| `/^a...s$/` | `abyss` | Match |
| `/^a...s$/` | `Alias` | No match |
| `/^a...s$/` | `An abacus` | No match |

## Create a RegEx

There are two ways you can create a regular expression in JavaScript.

### 1. Using a regular expression literal:

The regular expression consists of a pattern enclosed between slashes `/`. For example,

```jsx
cost regularExp = /abc/;
```

Here, `/abc/` is a regular expression.

### 2. **Using the** `RegExp()` **constructor function**:

You can also create a regular expression by calling the `RegExp()` constructor function.

For example,

```jsx
const reguarExp = new RegExp('abc');
```

For example,

```jsx
const regex = new RegExp(/^a...s$/);
console.log(regex.test('alias')); // true
```

In the above example, the string `alias` matches with the RegEx pattern `/^a...s$/`. Here, the `test()` method is used to check if the string matches the pattern.

There are several other methods available to use with JavaScript RegEx. Before we explore them, let's learn about regular expressions themselves.

## Specify Pattern Using RegEx

To specify regular expressions, metacharacters are used. In the above example (`/^a...s$/`), `^` and `$` are metacharacters.

## MetaCharacters

Metacharacters are characters that are interpreted in a special way by a RegEx engine. Here's a list of metacharacters:

```jsx
[] . ^ $ * + ? {} () \ |
```

### **`[]`** **- Square brackets**

Square brackets specify a set of characters you wish to match.

| Expression | String | Matched? |
| --- | --- | --- |
| `[abc]` | `a` | 1 match |
| `[abc]` | `ac` | 2 matches |
| `[abc]` | `Hey Jude` | No match |
| `[abc]` | `abc de ca` | 5 matches |

Here, `[abc]` will match if the string you are trying to match contains any of the `a`, `b` or `c`.
You can also specify a range of characters using `-` inside square brackets.

`[a-e]` is the same as `[abcde]`.

`[1-4]` is the same as `[1234]`.

`[0-39]` is the same as `[01239]`.

You can complement (invert) the character set by using caret `^` symbol at the start of a square-bracket.

`[^abc]` means any character except `a` or `b` or `c`.

`[^0-9]` means any non-digit character.

### `.` **- Period**

A period matches any single character (except newline `'\n'`).

| Expression | String | Matched? |
| --- | --- | --- |
| `..` | `a` | No match |
| `..` | `ac` | 1 match |
| `..` | `acd` | 1 match |
| `..` | `acde` | 2 matches (contains 4 characters) |

### **`^`** **- Caret**

The caret symbol `^` is used to check if a string **starts with** a certain character.

| Expression | String | Matched? |
| --- | --- | --- |
| `^a` | `a` | 1 match |
| `^a` | `abc` | 1 match |
| `^a` | `bac` | No match |
| `^ab` | `abc` | 1 match |
| `^ab` | `acb` | No match (starts with `a` but not followed by `b`) |

### **`$`** **- Dollar**

The dollar symbol `$` is used to check if a string **ends with** a certain character.

| Expression | String | Matched? |
| --- | --- | --- |
| `a$` | `a` | 1 match |
| `a$` | `formula` | 1 match |
| `a$` | `cab` | No match |

### **`*`** **- Star**

The star symbol `*` matches **zero or more occurrences** of the pattern left to it.

| Expression | String | Matched? |
| --- | --- | --- |
| `ma*n` | `mn` | 1 match |
| `ma*n` | `man` | 1 match |
| `ma*n` | `mann` | 1 match |
| `ma*n` | `main` | No match (`a` is not followed by `n`) |
| `ma*n` | `woman` | 1 match |

### **`+`** **- Plus**

The plus symbol `+` matches one or more occurrences of the pattern left to it.

| Expression | String | Matched? |
| --- | --- | --- |
| `ma+n` | `mn` | No match (no `a` character) |
| `ma+n` | `man` | 1 match |
| `ma+n` | `mann` | 1 match |
| `ma+n` | `main` | No match (`a` is not followed by `n`) |
| `ma+n` | `woman` | 1 match |

### **`?`** **- Question Mark**

The question mark symbol `?` matches **zero or one occurrence** of the pattern left to it.

| Expression | String | Matched? |
| --- | --- | --- |
| `ma?n` | `mn` | 1 match |
| `ma?n` | `man` | 1 match |
| `ma?n` | `maan` | No match (more than one `a` character) |
| `ma?n` | `main` | No match (`a` is not followed by `n`) |
| `ma?n` | `woman` | 1 match |

### **`{}`** **- Braces**

Consider this code: `{n,m}`. This means at least `n`, and at most `m` repetitions of the pattern left to it.

| Expression | String | Matched? |
| --- | --- | --- |
| `a{2,3}` | `abc dat` | No match |
| `a{2,3}` | `abc daat` | 1 match (at `daat`) |
| `a{2,3}` | `aabc daaat` | 2 matches (at `aabc` and `daaat`) |
| `a{2,3}` | `aabc daaaat` | 2 matches (at `aabc` and `daaaat`) |

Let's try one more example. This RegEx `[0-9]{2, 4}` matches at least 2 digits but not more than 4 digits.

| Expression | String | Matched? |
| --- | --- | --- |
| `[0-9]{2,4}` | `ab123csde` | 1 match (match at `ab123csde`) |
| `[0-9]{2,4}` | `12 and 345673` | 3 matches (`12`, `3456`, `73`) |
| `[0-9]{2,4}` | `1 and 2` | No match |

### **`|`** - Alternation

Vertical bar `|` is used for alternation (`or` operator).

| Expression | String | Matched? |
| --- | --- | --- |
| `a|b` | `cde` | No match |
| `a|b` | `ade` | 1 match (match at `ade`) |
| `a|b` | `acdbea` | 3 matches (at `acdbea`) |

Here, `a|b` match any string that contains either `a` or `b`

### **`()`** **- Group**

Parentheses `()` is used to group sub-patterns. For example, `(a|b|c)xz` match any string that matches either `a` or `b` or `c` followed by `xz`

| Expression | String | Matched? |
| --- | --- | --- |
| `(a|b|c)xz` | `ab xz` | No match |
| `(a|b|c)xz` | `abxz` | 1 match (match at `abxz`) |
| `(a|b|c)xz` | `axz cabxz` | 2 matches (at `axzbc` `cabxz`) |

### **`\`** **- Backslash**

Backslash `\` is used to escape various characters including all metacharacters. For example,

`\$a` match if a string contains `$` followed by `a`. Here, `$` is not interpreted by a RegEx engine in a special way.

If you are unsure if a character has special meaning or not, you can put `\` in front of it. This makes sure the character is not treated in a special way.

## Special Sequences

Special sequences make commonly used patterns easier to write. Here's a list of special sequences:

`\A` - Matches if the specified characters are at the start of a string.

| Expression | String | Matched? |
| --- | --- | --- |
| `\Athe` | `the sun` | Match |
| `\Athe` | `In the sun` | No match |

`\b` - Matches if the specified characters are at the beginning or end of a word.

| Expression | String | Matched? |
| --- | --- | --- |
| `\bfoo` | `football` | Match |
| `\bfoo` | `a football` | Match |
| `foo\b` | `a football` | No match |
| `foo\b` | `the foo` | Match |
| `foo\b` | `the afoo test` | Match |
| `foo\b` | `the afootest` | No match |

`\B` - Opposite of `\b`. Matches if the specified characters are not at the beginning or end of a word.

| Expression | String | Matched? |
| --- | --- | --- |
| `\Bfoo` | `football` | No match |
| `\Bfoo` | `a football` | No match |
| `foo\B` | `a football` | Match |
| `foo\B` | `the foo` | No match |
| `foo\B` | `the afoo test` | No match |
| `foo\B` | `the afootest` | Match |

`\d` - Matches any decimal digit. Equivalent to `[0-9]`

| Expression | String | Matched? |
| --- | --- | --- |
| `\d` | `12abc3` | 3 matches (at `12abc3`) |
| `\d` | `JavaScript` | No match |

`\D` - Matches any non-decimal digit. Equivalent to `[^0-9]`

| Expression | String | Matched? |
| --- | --- | --- |
| `\D` | `1ab34"50` | 3 matches (at `1ab34"50`) |
| `\D` | `1345` | No match |

`\s` - Matches where a string contains any whitespace character. Equivalent to `[ \t\n\r\f\v]`.

| Expression | String | Matched? |
| --- | --- | --- |
| `\s` | `JavaScript RegEx` | 1 match |
| `\s` | `JavaScriptRegEx` | No match |

`\S` - Matches where a string contains any non-whitespace character. Equivalent to `[^ \t\n\r\f\v]`.

| Expression | String | Matched? |
| --- | --- | --- |
| `\S` | `a b` | 2 matches (at `a` `b`) |
| `\S` |  | No match |

`\w` - Matches any alphanumeric character (digits and alphabets). Equivalent to `[a-zA-Z0-9_]`. By the way, underscore `_` is also considered an alphanumeric character.

| Expression | String | Matched? |
| --- | --- | --- |
| `\w` | `12&": ;c` | 3 matches (at `12&": ;c`) |
| `\w` | `%"> !` | No match |

`\W` - Matches any non-alphanumeric character. Equivalent to `[^a-zA-Z0-9_]`

| Expression | String | Matched? |
| --- | --- | --- |
| `\W` | `1a2%c` | 1 match (at `1a2%c`) |
| `\W` | `JavaScript` | No match |

`\Z` - Matches if the specified characters are at the end of a string.

| Expression | String | Matched? |
| --- | --- | --- |
| `JavaScript\Z` | `I like JavaScript` | 1 match |
| `JavaScript\Z` | `I like JavaScript Programming` | No match |
| `JavaScript\Z` | `JavaScript is fun` | No match |

## Regular Expression Methods

As mentioned above, you can either use `RegExp()` or regular expression literal to create a RegEx in JavaScript.

```jsx
const regex1 = /^ab/;
const regex2 = new Regexp('/^ab/');
```

In JavaScript, you can use regular expressions with `RegExp()` methods: `test()` and `exec()`.
There are also some string methods that allow you to pass RegEx as its parameter. They are: `match()`, `replace()`, `search()`, and `split()`.

| Method | Description |
| --- | --- |
| `exec()` | Executes a search for a match in a string and returns an array of information. It returns null on a mismatch. |
| `test()` | Tests for a match in a string and returns true or false. |
| match() | Returns an array containing all the matches. It returns null on a mismatch. |
| matchAll() | Returns an iterator containing all of the matches. |
| search() | Tests for a match in a string and returns the index of the match. It returns -1 if the search fails. |
| replace() | Searches for a match in a string and replaces the matched substring with a replacement substring. |
| split() | Break a string into an array of substrings. |

## Example 1: Regular Expressions

```jsx
const string = 'Find me';
const pattern = /me/;

// search if the pattern is in string variable
const result1 = string.search(pattern);
console.log(result1); // 5

// replace the character with another character
const string1 = 'Find me';
string1.replace(pattern, 'found you'); // Find found you

// splitting strings into array elements
const regex1 = /[\s,]+/;
const result2 = 'Hello world! '.split(regex1);
console.log(result2); // ['Hello', 'world!', '']

// searching the phone number pattern
const regex2 = /(\d{3})\D(\d{3})-(\d{4})/g;
const result3 = regex2.exec('My phone number is: 555 123-4567.');
console.log(result3); // ["555 123-4567", "555", "123", "4567"]
```

## Regular Expression Flags

Flags are used with regular expressions that allow various options such as global search, case-insensitive search, etc. They can be used separately or together.

| Flags | Description |
| --- | --- |
| `g` | Performs a global match (find all matches) |
| `m` | Performs multiline match |
| `i` | Performs case-insensitive matching |

## Example 2: Regular Expression Modifier

```jsx
const string = 'Hello hello hello';

// performing a replacement
const result1 = string.replace(/hello/, 'world');
console.log(result1); // Hello world hello

// performing global replacement
const result2 = string.replace(/hello/g, 'world');
console.log(result2); // Hello world world

// performing case-insensitive replacement
const result3 = string.replace(/hello/i, 'world');
console.log(result3); // world hello hello

// performing global case-insensitive replacement
const result4 = string.replace(/hello/gi, 'world');
console.log(result4); // world world world
```