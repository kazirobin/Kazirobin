# SVG Text

`<text>` element is used to draw text.

Following is the syntax declaration of `<text>` element. We've shown main attributes only.

```html
<text
  x="x-cordinates"
  y="y-cordinates"
  
  dx="list of lengths"
  dy="list of lengths"
  
  rotate="list of numbers"
  textlength="length"
  lengthAdjust="spacing" >
</text>
```

## Attributes

1. `x` − x axis coordinates of glyphs.
2. `y` − y axis coordinates of glyphs.
3. **`dx`** − shift along with x-axis.
4. `dy` − shift along with y-axis.
5. `rotate` − rotation applied to all glyphs.
6. `textlength` − rendering length of the text.
7. `lengthAdjust` − type of adjustment with the rendered length of the text.

### Text #1 : Example

```html
<html>
   <title>SVG Text</title>
   <body>
      
      <h1>Sample SVG Text</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="30" y="12" >Text: </text>
            <text x="30" y="30" fill="rgb(121,0,121)">WWW.TutorialsPoint.COM</text>
         </g> 
      </svg>
   
   </body>
</html>
```

### Text #2 : With Rotate

```html
<html>
   <title>SVG Text</title>
   <body>
   
      <h1>Sample SVG Text</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="30" y="12" >Multiline Text: </text>
            <text x="30" y="30" fill="rgb(121,0,121)">WWW.TutorialsPoint.COM
            <tspan x="30" y="50" font-weight="bold">Simply Easy learning.</tspan>
            <tspan x="30" y="70">We teach just for free.</tspan>
            </text>
         </g>
      </svg>
      
   </body>
</html>
```

### Text #3 : With Multiline Text

```html
<html>
   <title>SVG Text</title>
   <body>
   
      <h1>Sample SVG Text</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="30" y="12" >Multiline Text: </text>
            <text x="30" y="30" fill="rgb(121,0,121)">WWW.TutorialsPoint.COM
            <tspan x="30" y="50" font-weight="bold">Simply Easy learning.</tspan>
            <tspan x="30" y="70">We teach just for free.</tspan>
            </text>
         </g>
      </svg>
      
   </body>
</html>
```

### Text #4 : With **Hyper link Text**

```html
<html>
   <title>SVG Text</title>
   <body>
   
      <h1>Sample SVG Text</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="30" y="10" >Text as Link: </text>
         
            <a xlink:href="http://www.tutorialspoint.com/svg/" target="_blank">
               <text font-family="Verdana" font-size="20"  x="30" y="30" 
               fill="rgb(121,0,121)">WWW.TutorialsPoint.COM</text>
            </a>
         </g>
      </svg>
      
   </body>
</html>
```