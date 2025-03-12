# Pseudo Element Selectors

Pseudo-element selectors are used for styling a specific part of an element - you can use them to insert new content or change the look of a specific section of the content.

For example, you can use a pseudo-element to style the first letter or the first line of an element differently. You can also use pseudo-elements to add new content before or after the selected element.

In contrast to pseudo-classes that are preceded by a `:` character, pseudo-elements are preceded by a `::` character.

The `::` character is followed by a keyword that allows you to style a specific part of the selected element.

The general syntax looks something like the following:

```css
element::pseudo-element-selector {
    property:value;
}
```

Make sure to use the `::` character instead of the `:` one when using pseudo-element selectors - this will help distinguish pseudo-classes from pseudo-elements.

Now, let's see some of the most common pseudo-elements you will encounter.

## The `::before` Pseudo-Element

You can use the `::before` pseudo-element to insert content before an element:

```css
p::before {
    property: value;
}
```

## The `::after` Pseudo-Element

And you can use the `::after` pseudo-element to insert content at the end of an element:

```css
p::after {
    property: value;
}
```

## The `::first-letter` Pseudo-Element

You can also use the `::first-letter` pseudo-element to select the first letter of a paragraph, which is helpful when you want to style the first letter in a certain way:

```css
p::first-letter {
    property: value;
}
```

## The `::first-line` Pseudo-Element

And you can use the `::first-line` pseudo-element to select the first line of a paragraph:

```css
p::first-line {
    property: value;
}
```