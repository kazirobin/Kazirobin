# Grouping CSS Selector

With the grouping selector, you can target and style more than one element at once.

To use the grouping selector, use a comma, `,` to group and separate the different elements you want to select.

For example, here is how you would target multiple elements such as `div`s, `p`s, and `span`s all at once and apply the same styles to each of them:

```css
div, p, span {
    property: value;
}
```

The code above matches all `div`, `p`, and `span` elements on the page, and those three elements will share the same styling.