# CSS Attribute Selectors

Many HTML elements have attributes.

HTML attributes:

- Provide additional information about HTML elements.
- Are always specified in the start (or opening) tag.
- Usually come in name/value pairs such as `name="value"`.
- The `value` in a name/value pair should be enclosed in quotation marks.

One of the most popular HTML attributes you may have come across is the `href` attribute, which is added to the opening `<a>` tag and specifies the URL the `<a>` tag links to:

```css
<a href="https://www.freecodecamp.org/">The best place to learn to code for free!</a>
```

The value of the `href`, `https://www.freecodecamp.org/`, is the URL the user will be taken to when they click on the link text, `The best place to learn to code for free!`.

The attribute selector matches and selects HTML elements based on the presence of an attribute or a specific attribute value.

There are different types of attribute selectors.

## The `[attribute]` Selector

To use the attribute selector, use a pair of square brackets, `[]`, to select the attribute you want.

The general syntax for attribute selectors is the following:

```css
element[attribute]
```

## The `[attribute="value"]` Selector

You can specify the value of the attribute using the following syntax:

```css
element[attribute="value"]
```

So, if you want to style `a` elements with an `attr` attribute that has an **exact** value of `1`, you would do the following:

```css
a[attr="1"] {
    property: value;
}
```

This code above matches `a` elements where the `attr` attribute name has an exact value of `1`.

## The `[attribute^="value"]` Selector

You could also specify that the value of the attribute **starts** with a specific character using the following syntax:

```css
element[attribute^="value"]
```

For example, if you wanted to select and style any `a` elements that have an `attr` attribute with a value that starts with `www`, you would do the following:

```css
a[attr^="www"] {
    property: value;
}
```

The code above selects any `a` elements where the `attr` attribute name has a value that starts with `www`.

## The `[attribute$="value"]` Selector

You could also specify that the value of the attribute **ends** with a specific character using the following syntax:

```css
element[attribute$="value"]
```

For example, if you wanted to select `a` elements that have an `attr` attribute name with a value that ends with `.com`, you would do the following:

```css
a[attr$=".com"] {
    property: value;
}
```

## The `[attribute*="value"]` Selector

You can also specify that the attribute value contains a specific substring - this selector is known as the Attribute Contains Substring Selector and has the following syntax:

```css
element[attribute*="value"]
```

In this case, the string `value` needs to be present in the attribute's value followed by any number of other characters - `value` doesn't need to be a whole word.

For example, if you wanted to select `a` elements that have an `attr` attribute with a value that contains the string `free`, you would do the following:

```css
a[attr*="free"] {
    property:value;
}
```

The code above selects `a` elements with an `attr` attribute name when the string `free` is present in the attribute's value - even as a substring (a substring is a word inside another word).

As long as the attribute's value contains `free`, then the HTML element is selected - this could match an `attr` attribute with a value of `free`, `freeCodeCamp`, or `freediving`, for example.

## The `[attribute~="value"]` Selector

You can also specify that the selector matches an attribute value that contains a whole word using the following syntax:

```css
element[attribute~= "value"]
```

In this case, the string `value` needs to be a whole word.

For example, if you wanted to select `a` elements that have an `attr` attribute name with a value that contains the word `free`, you would do the following:

```css
a[attr~= "free"] {
    property: value;
}
```

The code above would match an `attr` attribute with a value of `free` that contains different kinds of whitespace.

The code wouldn't select elements with an `attr` value of `freeCodeCamp` or `freediving` like you saw in an earlier example because `free` needs to be a whole word on its own - not a substring.