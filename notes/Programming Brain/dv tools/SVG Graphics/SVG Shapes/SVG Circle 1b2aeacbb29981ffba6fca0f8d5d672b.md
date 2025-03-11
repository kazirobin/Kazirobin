# SVG Circle

`<circle>` element is used to draw circle with a center point and given radius.

Following is the syntax declaration of `<circle>` element. We've shown main attributes only.

```html
<circle
   cx="x-axis co-ordinate"
   cy="y-axis co-ordinate"
   r="length" >   
</circle>
```

## Attributes

1. `cx` − x-axis co-ordinate of the center of the circle. Default is 0.
2. `cy` − y-axis co-ordinate of the center of the circle. Default is 0.
3. `r` − radius of the circle.

### Circle #1: Without Opacity

```html
<html>
   <title>SVG Circle</title>
   <body>
      
      <h1>Sample SVG Circle Image</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="0" y="15" fill="black" >Circle #1: Without opacity.</text>
            <circle cx="100" cy="100" r="50" stroke="black" 
            stroke-width="3" fill="rgb(121,0,121)"></circle>
         </g> 
      </svg>
      
   </body>
</html>
```

### Circle #2: With Opacity

```html
<html>
   <title>SVG Circle</title>
   <body>
   
      <h1>Sample SVG Circle Image</h1>
      
      <svg width="800" height="800"> 
         <g>
            <text x="0" y="15" fill="black" >Circle #2: With opacity </text>
            <circle cx="100" cy="100" r="50"
            style="fill:rgb(121,0,121);stroke-width:3;
            stroke:rgb(0,0,0);stroke-opacity:0.5;opacity:0.5"> </circle>
         </g>
      </svg>
   
   </body>
</html>
```