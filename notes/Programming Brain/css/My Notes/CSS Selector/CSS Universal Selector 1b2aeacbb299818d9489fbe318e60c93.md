# CSS Universal Selector

The universal selector, also known as a wildcard, selects everything - every single element in the document.

To use the universal selector, use the asterisk character, `*`.

```css
* {
    property: value;
}
```

You can use the universal selector to reset the browser's default padding and margin to zero at the top of the file before you add any other styles:

```css
* {
    padding: 0;
    margin:  0;
}
```