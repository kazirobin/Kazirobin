# DOM Selector

Selecting DOM (Document Object Model) elements is a fundamental aspect of web development with JavaScript. It allows developers to interact with and manipulate elements on a webpage dynamically. Proper selection of elements is crucial for tasks such as updating content, adding event listeners, or modifying styles.

DOM Selectors, as the name suggests is used to **select HTML elements within a document** using JavaScript. There are **5** ways in which you can select elements in a DOM using selectors.

- `getElementsByTagName()`
- `getElementsByClassName()`
- `getElementById()`
- `querySelector()`
- `querySelectorAll()`

## Universal Selector

The universal selector is denoted by `*` that matches all elements of any type, The following example uses the querySelector() selects the first element in the document:

```jsx
let element = document.querySelector('*');
```

## Type Selector

To select elements by node name, you use the type selector e.g., a selects all `<a>` elements, The following example finds the first `a` element in the document:

```jsx
let anchor = document.querySelector('a');
```

## Class Selector

To find the element with a given CSS class, you use the class selector, The following example finds the first element with the `menu-item` class:

```jsx
let note = document.querySelector('.menu-item');
```

## ID Selector

To select an element based on the value of its id, you use the id selector, The following example finds the first element with the id `#logo`:

```jsx
let logo = document.querySelector('#logo');
```

Since the id should be unique in the document, the `querySelectorAll()` is not relevant.

## Attribute Selector

To select all elements that have a given attribute, you use one of the following attribute selector syntaxes:

```jsx
[attribute]
[attribute=value]
[attribute~=value]
[attribute|=value]
[attribute^=value]
[attribute$=value]
[attribute*$*=value]
```

The following example finds the first element with the attribute `[autoplay]` with any value:

```jsx
let autoplay = document.querySelector('[autoplay]');
```

## Grouping Selectors

To group multiple selectors, you use the following syntax,  The selector list will match any element with one of the selectors in the group.

The following example finds all `<div>` and `<p>` elements:

```jsx
let elements = document.querySelectorAll('div, p');
```

## Combinators

### 1) descendant combinator

To find descendants of a node, you use the space ( ) descendant combinator syntax:

```jsx
selector selector
```

For example `p` a will match all `<a>` elements inside the p element:

```jsx
let links = document.querySelector('p a');
```

### 2) Child combinator

The `>` child combinator finds all elements that are direct children of the first element:

```jsx
selector > selector
```

The following example finds all li elements that are directly inside a <ul> element:

```jsx
let listItems = document.querySelectorAll('ul > li');
```

To select all li elements that are directly inside a <ul> element with the class nav:

```jsx
let listItems = document.querySelectorAll('ul.nav > li');
```

### 3) General sibling combinator

The `~` combinator selects siblings that share the same parent:

```jsx
selector ~ selector
```

For example, p ~ a will match all <a> elements that follow the p element, immediately or not:

```jsx
let links = document.querySelectorAll('p ~ a');
```

### 4) Adjacent sibling combinator

The `+` adjacent sibling combinator selects adjacent siblings:

```jsx
selector + selector
```

For example, h1 + a matches all elements that directly follow an h1:

```jsx
let links = document.querySelectorAll('h1 + a');
```

And select the first <a> that directly follows an h1:

```jsx
let links = document.querySelector('h1 + a');
```

## Pseudo

### 1) Pseudo-classes

The `:` pseudo matches elements based on their states:

```jsx
element:state
```

For example, the li:nth-child(2) selects the second <li> element in a list:

```jsx
let listItem = document.querySelectorAll('li:nth-child(2)');
```

### 2) Pseudo-elements

The `::` represent entities that are not included in the document.

For example, p::first-line matches the first line of all p elements:

```jsx
let links = document.querySelector('p::first-line');
```