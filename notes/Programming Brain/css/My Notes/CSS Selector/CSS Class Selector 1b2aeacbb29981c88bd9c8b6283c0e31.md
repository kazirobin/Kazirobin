# CSS Class Selector

The class selector matches and selects HTML elements based on the value of their given class. Specifically, it selects every single element in the document with that specific class name.

With the class selector, you can select multiple elements at once and style them the same way without copying and pasting the same styles for each one separately.

Classes are reusable, making them a good option for practicing DRY development. DRY is a programming principle and is short for 'Don't Repeat Yourself'. As the name suggests, the aim is to avoid writing repetitive code whenever possible.

To select elements with the class selector, use the dot character, `.`, followed by the name of the class.

```css
.my_class {
    property: value;
}
```

In the code above, elements with a class of `my_class` are selected and styled accordingly.