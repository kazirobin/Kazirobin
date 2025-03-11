# PX, REM, EM

The main differences between `px`, `rem`, and `em` in CSS are based on how they scale and relate to other elements.

## px (Pixels)

- **Fixed size**: `px` is an absolute unit that represents a specific number of pixels on the screen.
- **Does not scale**: It remains the same regardless of the parent or root element’s font size.
- **Use case**: Best for elements that should not change in size (e.g., borders, images).

```css
p {
  font-size: 16px;
}
```

## rem (Root EM)

- **Relative to the root element (`<html>` tag)**: `1rem` equals the font size of the root `<html>` element.
- **Scales consistently**: If the root font size changes, all `rem`based values will scale proportionally.
- **Use case**: Ideal for creating consistent and scalable layouts.

```css
html {
  font-size: 16px; /* Default browser font size */
}

p {
  font-size: 2rem; /* 2 × 16px = 32px */
}
```

## em (Relative to Parent)

- **Relative to the font size of the parent element**.
- **Nesting can affect size**: If an element with `1.5em` is inside another element with `1.5em`, it compounds (1.5 × 1.5 = 2.25em).
- **Use case**: Useful for elements that should scale relative to their parent, such as buttons inside different-sized containers.

```css
div {
  font-size: 20px;
}

p {
  font-size: 1.5em; /* 1.5 × 20px = 30px */
}
```

## Key Differences

| Unit | Based On | Scales With | Best Use Case |
| --- | --- | --- | --- |
| `px` | Fixed screen pixels | No scaling | Fixed-size elements |
| `rem` | Root (`html`) font size | Consistent scaling | Global typography |
| `em` | Parent element font size | Nested scaling | Local component-based scaling |

## Which One to Use?

- Use **`rem`** for global font sizes and spacing (ensures consistent scaling).
- Use **`em`** for elements that should scale relative to their parent.
- Use **`px`** for elements that need a fixed size.