# CSS Units

CSS units define the size, length and measurement of the web elements. For example,

```css
p {
    width: 300px;
    background-color: greenyellow;
}
```

### Browser Output

![css-units-introduction-example.png](CSS%20Units%201b2aeacbb29981d6adb8fbad804de41a/css-units-introduction-example.png)

Here, we have specified the `width` value of the paragraph with a pixel (`px`) length unit.

There are various CSS properties such as `width`, `padding`, `margin`, etc. that accept measurement values in various units.

CSS units are mainly categorized as absolute and relative units.

## Absolute Units

Absolute units are the constant measurements that remain unchanged regardless of the device's screen size.

There are following types of absolute units:

- **Pixels (px)**: Equivalent to one pixel on the screen. For example, `width: 100px`.
- **Inches (in)**: Correspond to one inch in physical size. For example, `height: 1in`.
- **Centimeters (cm)**: Equivalent to one centimeter. For example, `margin: 2cm`.
- **Millimeters (mm)**: Equivalent to one millimeter. For example, `padding: 5mm`.
- **Points (pt)**: Equal to one point (1/72 of an inch). For example, `font-size: 12pt`.

Absolute units are used for elements that need to have a specific size, such as buttons, images, and logos.

**Note:** Absolute units are preferred for providing specific and consistent sizes which ensures uniform display across devices.

## Relative Units

Relative units are the measurements that change with the screen size or other elements on the page.

There are following types of relative units:

- **Ems (em)**: Relative to the parent element's font size. For example, `font-size: 1em` scales with the parent's font size.

If the parent has a font size of `16px`, then `font-size:1em` for a child equals `16px`.

- **Rems (rem)**: Relative to the root element's font size i.e. size set to HTML element. For example, `margin: 2rem` adjusts based on the root font size.
- **Viewport widths (vw)**: Relative to the viewport width. For example, `width: 50vw` adapts to 50% of the viewport's width.
- **Viewport heights (vh)**: Relative to the viewport height. For example, `height: 100vh` takes up the entire viewport (screen) height.
- **Percentages (%):** Relative to the containing element. For example, `padding: 5%` scales based on the parent container's size.

Relative units are preferred when we need flexible sizing and responsive design across various devices.

For example,

```css
body {
    height: 80vh;
}
```

This sets the height of the `body` element to `80%` of the total height of the device's screen (viewport).

## Example: Absolute Unit

Let's look at an example of using pixel (`px`).

```css
div.box {
    width: 100px;
    height: 100px;
    background-color: red;
}
```

### Browser Output

![css-pixels-example.png](CSS%20Units%201b2aeacbb29981d6adb8fbad804de41a/css-pixels-example.png)

In the above example, the `width` and `height` of the `div` element are set fixed to `100` pixels, regardless of the screen size.

## Example: Relative Unit

Let's look at an example of using percentage (`%`).

```css
div.parent {
    width: 400px;
    height: 100px;
    background-color: skyblue;
    border: 2px solid black;
}

div.child {
    width: 50%;
    height: 50%;
    background-color: orange;
}
```

### Browser Output

![css-percentage-example.png](CSS%20Units%201b2aeacbb29981d6adb8fbad804de41a/css-percentage-example.png)

In the above example,

```css
div.child {
    width: 50%;
    height: 50%;
}
```

sets the `width` and `height` of the child div to `50%` of the parent `div` element.
This means that the child element will always be `50%` as wide and as high as the parent element.