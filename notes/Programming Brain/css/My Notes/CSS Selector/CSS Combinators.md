# CSS Combinators

Combinators allow you to combine two elements based on the relationship between the elements and their location in the document.

Essentially, you can combine two simple selectors in a way that explains the relationship between those CSS selectors. Combinators are a type of selector that specifies and describes the relationship between the two selectors.

There are four types of combinators:

- The descendant combinator.
- The direct child combinator.
- The general sibling combinator.
- The adjacent sibling combinator

As the name implies, the descendant combinator selects only the descendants of the specified element.

Essentially, you first mention the parent element, leave a space, and then mention the descendant of the first element, which is the child element of the parent. The child element is an element inside the parent element.

Let's take the following as an example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="main.css">
  <title>Document</title>
</head>
<body>
  <div>
    <h2>I am level 2 heading</h2>
    <p>I am a paragraph inside a div</p>
    <span>I am a span</span>
    <p>I am a paragraph inside a div</p>
  </div>
  <p>I am a paragraph outside a div</p>
</body>
</html>
```

In the example above, the `div` is the parent, and the `h2`, `span`, and two `p` are the child elements because they are inside the `div`. There is also a paragraph outside the `div`.

If you wanted to style only the paragraphs that are inside the `div`, here is what you would do:

```css
div p {
    property: style;
}
```

In the example above, only the two paragraphs inside the `div` that have the text `I am a paragraph inside a div` get styled. The other two child elements and the paragraph outside the `div` with the text `I am a paragraph outside a div` do not get styled.

## Direct Child Combinator

The direct child combinator, also known as the direct descendant, selects only the direct children of the parent.

To use the direct child combinator, specify the parent element, then add the `>` character followed by the direct children of the parent element you want to select.

Let's take the following as an example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="main.css">
  <title>Document</title>
</head>
<body>
  <div>
    <a href="#">I am a link</a>
    <a href="#">I am a link</a>
    <p><a href="#">I am a link inside a paragraph</a></p>
  </div>
</body>
</html>
```

There is a `div` which is the parent element.

Inside the parent element, there are two `a` elements which are the direct children of the `div`.

There is also another `a` element inside a `p` element. The `p` element is a child of the `div`, but the `a` element inside the paragraph is *not* a direct child of the `div`.

So, to access only the `a` elements that are direct children of `div`, you would do the following:

```css
div > a  {
    property: value;
}
```

The code above matches the `a` elements directly nested inside the `div` element and are immediate children.

## General Sibling Combinator

The general sibling combinator selects siblings.

You can specify the first element and a second one that comes after the first one. The second element doesn't need to come right after the first one.

To use the general sibling combinator, specify the first element, then use the `~` character followed by the second element that needs to follow the first one.

Let's take the following as an example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="main.css">
  <title>Document</title>
</head>
<body>
  <div>
    <p>I am paragraph inside a div</p>
  </div>
  <p>I am a paragraph outside a div</p>
  <h3>I am a level three heading</h3>
  <p>I am a paragraph outside a div</p>
</body>
</html>
```

The `div` has a `p` element nested inside it. That specific `p` element is a child of `div`.

There are also two paragraphs with the text `I am a paragraph outside a div` and an `h3` element. All those three elements are siblings of the `div` element.

So, to select the `p` elements that are siblings of the `div` element, you would do the following

```html
div ~ p {
    property: value;
}
```

## Adjacent Sibling Combinator

The adjacent sibling combinator is more specific than the general sibling combinator.

This selector matches only the immediate siblings. Immediate siblings are the siblings that come right after the first element.

To use the adjacent sibling combinator, specify the first element, then add the `+` character followed by the element you want to select that immediately follows the first element.

Let's revisit the example from the previous section:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="main.css">
  <title>Document</title>
</head>
<body>
  <div>
    <p>I am paragraph inside a div</p>
  </div>
  <p>I am a paragraph outside a div</p>
  <h3>I am a level three heading</h3>
  <p>I am a paragraph outside a div</p>
</body>
</html>
```

Although the `p` element that follows the `h3` element is a sibling of the `div` element, it is not a direct sibling like the `p` element that comes before the `h3`.

So, to target only the `p` element that comes directly after the `div`, you would do the following:

```html
div + p {
    property: value;
}
```