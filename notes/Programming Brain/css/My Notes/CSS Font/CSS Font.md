# CSS Font

CSS font properties are used to adjust the appearance of the text in an HTML document. Using the CSS fonts properties, we can customize the font family, size, weight, style, and color of text.

```css
body {
  font-family: Helvetica;
  font-size: 16px;
}
```

Here,

- `font-family: Helvetica` - sets the font family of text to `Helvetica` within the body
- `font-size: 16px` - sets the font size of the text to `16px` within the body

## Basic Font Properties

In CSS, we have the following seven important font properties that are used to change different attributes of the text.

- `font-family`: defines the font applied to the text
- `font-size`: sets the size of the font
- `font-weight`: sets the thickness i.e increase the boldness or lightness of the font
- `font-style`: sets the font to italic or oblique
- `font-variant`: changes the font to small-caps
- `font-stretch`: expands or narrows the text
- `line-height`: sets the distance between lines of the text

We will learn about each of them in detail.

## CSS Font Family

CSS `font-family` property is used to set the font face of the text on the webpage. For example,

```css
h1 {
    font-family: Courier, monospace;
}
```

### Browser Output

![css-font-family.png](./CSS%20Font/css-font-family.png)

In the above example, we have set the font family of the `h1` element to the `Courier, monospace`. The browser tries to render the text of `h1` in `Courier` font, and if not available, `monospace` is rendered.

**Note:** It is recommended to list the family name in quotation marks when it consists of multiple words. For example, `"Times New Roman"`.

## CSS Font Size

CSS `font-size` property sets the size or height of the text. The values of `font-size` can be expressed by keywords, length units (`px`, `em`, `rem`, etc), or percentages. For example,

```css
h1 {
    /*sets the font size of h1 element to 36px */
    font-size: 42px;
}

p {
    /* sets the font size to p element to 24px */
    font-size: 24px;
}
```

### Browser Output

![css-font-size.png](./CSS%20Font/css-font-size.png)

## CSS Font Style

CSS `font-style` property is used to style a font either with a `normal`, `italic`, or `oblique` face. For example,

```css
h1.normal {
	font-style: normal;
}

h1.italic {
	font-style: italic;
}

h1.oblique {
	font-style: oblique;
}
```

### Browser Output

![css-font-style.png](./CSS%20Font/css-font-style.png)

The possible values for CSS `font-style` are as follows:

- `normal`: text is shown normally
- `italic`: text is shown in italics
- `oblique`: text is leaned which is very similar to italic

## CSS Font Stretch

CSS `font-stretch` property is used to widen or narrow the text by allowing us to select a `normal`, `expanded` or `condensed` face from the font's family. For example,

```css
body {
	font-family: Arial;
}
.condensed {
	font-stretch: condensed;
}

.expanded {
	font-stretch: expanded;
}
```

### Browser Output

![css-font-stretch.png](./CSS%20Font/css-font-stretch.png)

**Note:** This property has no effect if the selected font family does not offer condensed or expanded faces.

## CSS Font Variant

CSS `font-variant` is used to set the text to `small-caps` (uppercase letters but in smaller font size). For example,

```css
.normal {
    font-variant: normal;
}

.small-caps {
    font-variant: small-caps;
}
```

### Browser Output

![css-font-variant.png](./CSS%20Font/css-font-variant.png)

The possible values for CSS `font-variant` style are as follows:

- `normal`: default value and makes no change to the font
- `small-caps`: displays text in small uppercase letters
- `initial`: sets the text to initial value which is normal by default
- `inherit`: sets the text to value as of its parent element

## CSS Font Weight

CSS `font-weight` determines the lightness or boldness of the text. It can be specified by using numeric or pre-defined keywords such as `bold`, `lighter`, etc. For example,

```css
p.bold {
    font-weight: bold;
}
```

### Browser Output

![css-font-weight.png](./CSS%20Font/css-font-weight.png)

The weight available depends on the `font-family` that is currently set. If the specified `font-family` does not offer the requested font weight, the browser will simulate the lightness or boldness that approximates the requested weight.

## CSS Line Height

CSS `line-height` property is used to set the height of the line box. It allows setting the height of the line independently from the font size. For example,

```css
.normal-value {
    /* specifies the normal line height */
    line-height: normal;
}

.numeric-value {
    line-height: 1.5; /* sets value 1.5 times the current font size : 16px x 1.5 = 24px */
}
```

### Browser Output

![css-line-height.png](./CSS%20Font/css-line-height.png)

The possible values for CSS `line-height` are as follows:

| Line Height Values | Description |
| --- | --- |
| normal | default value, specifies the normal line height |
| number | specifies the number that is multiplied with the current font size to set the line height |
| length | sets the line height in `px`, `pt`, `cm`, etc |
| % | sets the line height in percent of the current font size |
| initial | sets the value to default value i.e `normal` |
| inherit | inherits the property value from its parent element |

## CSS Font ShortHand Property

The CSS `font` shorthand property is used to set multiple font related properties in a single declaration. This property helps to shorten the code by specifying all the font properties in one place.

The `font` property has the following syntax:

```css
font: font-style font-variant font-weight font-size/line-height font-family;
```

The `font` shorthand property needs at least `font-size` and `font-family` values to work.

The order of the values provided in the above shorthand `font` property must follow the specified ordering. Default values are used if other values are omitted.

Let's see an example,

```css
h1 {
    font: italic small-caps bold 24px/1.2 "Helvetica Neue", Helvetica, Arial,
        sans-serif;
}

/* The above code is equivalent to
    h1 {
      font-style: italic;
      font-variant: small-caps;
      font-weight: bold;
      font-size: 24px;
      line-height: 1.2;
      font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
    }
    */
```

### Browser Output

![css-font-shorthand.png](./CSS%20Font/css-font-shorthand.png)