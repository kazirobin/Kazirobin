# Pseudo Class Selectors

Pseudo-class selectors select elements that are in a specific state.

Some examples of the state the element can be in are:

- The element is being hovered over by the mouse pointer.
- The element is the first of its type.
- The link has been visited before from that specific browser.
- The link has *not* been visited before from that specific browser.
- The checkbox/radio button has been checked.

Pseudo-class selectors start with a colon,`:`, followed by a keyword that reflects the state of the specified element.

The general syntax looks something like the following:

```css
element:pseudo-class-name {
    property: value;
}
```

## Pseudo-Class Selectors for Links

There are selectors based on link state information.

The `:link` selector applies styling when the element has not been visited before:

```css
a:link {
    property: value;
}
```

The `:visited` selector applies when the element has been visited before in the current browser:

```css
a:visited {
    property: value;
}
```

The `:hover` selector applies when the mouse pointer hovers over an element:

```css
a:hover {
    property: value;
}
```

The `:focus` selector applies when a user has tabbed onto an element:

```css
a:focus {
    property:value;
}
```

The `:active` selector applies when the element is selected after being clicked on and after holding down a mouse button:

```css
a:active {
    property: value;
}
```

## Pseudo-Class Selectors for Inputs

The `:focus` selector you saw earlier for links is used for inputs as well:

```css
input:focus {
    property: value;
}
```

The `:required` selector selects inputs that are required. Inputs that are required have the `required` attribute.

```css
input:required {
    property: value;
}
```

The `:checked` selector selects checkboxes or radio buttons that have been checked:

```css
input:checked {
    property:value;
}
```

The `:disabled` selector selects inputs that are disabled. Disabled inputs have the `disabled` attribute. Many browsers style disabled inputs with a faded-out gray color by default:

```css
input:disabled {
    property:value;
}
```

## Pseudo-Class Selectors for Position

The first child selector, `:first-child`, selects the first element, which will be the first child inside the parent container.

For example, here is how you would select an `a` element when it is the first child in the parent container:

```css
a:first-child {
    property: value;
}
```

The last child selector, `:last-child`, selects the last element, which will be the last child inside the parent container.

Here is how you would select an `a` element when it is the last child in the parent container:

```css
a:last-child {
    property: value;
}
```

The `:nth-child()` selector selects a child element inside a container based on its position in a group of siblings.

It takes an integer as an argument and selects an element based on the given value. The general syntax for the selector looks something like this:

```css
a:nth-child(n) {
    property: value;
}
```

The `:nth-child()` selector is helpful when you want to select elements based on an expression, such as selecting even or odd elements:

```css
a:nth-child(even) {
    property: value;
}
```

The first of type selector, `:first-of-type`, selects elements that are the first of that specific type in the parent container.

For example, here is how you would select the first `p` inside a `div`:

```css
p:first-of-type {
    property: value;
}
```

The last of type selector, `:last-of-type`, selects elements that are the last of that specific type in the parent container.

For example, here is how you would select the last `p` inside a `div`:

```css
p:last-of-type {
    property: value;
}
```