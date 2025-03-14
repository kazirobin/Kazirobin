# CSS !important

The `!important` keyword is used to increase the priority of a CSS property. For example,

```css
/* HTML */
<p id="paragraph">This is a paragraph.</p>

/* CSS */
p#paragraph {
  color: green;
}

p {
  color: blue!important;
}
```

### Browser Output

![css-important-introduction-example.png](./CSS%20!important/css-important-introduction-example.png)

Here, we have two selectors (ID selector and element selector) to select and style the paragraph.

The ID selector has higher priority (specificity) than the element selector. However, the `!important` keyword overrides the other styles, resulting the paragraph in the `blue` color.

## Syntax of !important

The syntax for the `!important` keyword is as follows:

```css
property: value !important;
```

To use the `!important` keyword, we need to add it after the value of a CSS property.

For example, to make a `p` element have a `red` text color, we would use the following CSS:

```css
p {
  color: red !important;
}
```

This will ensure that the text color of the `p` element is `red`, even if there are other CSS rules that are more specific.

## Priority Level in CSS

In CSS, selectors have the following priority level, from highest to lowest:

- ID selectors
- Class selectors
- Attribute selectors
- Pseudo-class selectors
- Type selectors
- Universal selectors
- Inherited styles

This means that the styles provided by an ID selector will be applied even if other selectors have also applied styles to the element.

However, when we add `!important` to any style, it gets the highest priority among all. This means that it overrides all conflicting CSS styles, no matter how specific they are.

## CSS !Important Keyword

```css
/* class selector */
.paragraph {
    color: green;
}

/* id selector */
#unique {
    color: purple;
}

/* using !important on element selector */
p {
    color: red !important;
}
```

### Browser Output

![css-important-property-example.png](./CSS%20!important/css-important-property-example.png)

Here, all the `p` elements are displayed in `red` color.

This is because the `!important` keyword in the element selector overrides other higher priority rules.

Note: The `!important` keyword helps resolve style conflicts. However, it is not recommended for excessive use as it can complicate code debugging and maintenance