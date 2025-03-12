# SVG Rectangle

`<rect>` element is used to draw rectangle which is axis aligned with the current user co-ordinate system.

Following is the syntax declaration of **<rect>** element. We've shown main attributes only.

```html
<rect
   x="x-axis co-ordinate"
   y="y-axis co-ordinate"
   
   width="length"
   height="length"
   
   rx="length"
   ry="length"
   
   style="style information"
   class="style class" >
</rect>
```

## Attributes

1. `x` − x-axis co-ordinate of top left of the rectangle. Default is 0.
2. `y` − y-axis co-ordinate of top left of the rectangle. Default is 0.
3. `width` − width of the rectangle.
4. `height` − height of the rectangle.
5. `rx` − used to round the corner of the rounded rectangle.
6. `ry` − used to round the corner of the rounded rectangle.
7. `style` − used to specify inline styles.
8. `class` − used to specify external style name to the element.

### **Rectangle #1 :** Without Opacity

```html
<html>
   <title>SVG Rectangle</title>
   <body>
      
      <h1>Sample SVG Rectangle Image</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="0" y="15" fill="black" >
            Rectangle #1: Without opacity.</text>
            
            <rect x="100" y="30" width="300" height="100" 
            style="fill:rgb(121,0,121);stroke-width:3;stroke:rgb(0,0,0)"></rect> 
         </g> 
      </svg>
   
   </body>
</html>
```

### **Rectangle #2 : With Opacity**

```html
<html>
   <title>SVG Rectangle</title>
   <body>
      
      <h1>Sample SVG Rectangle Image</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="0" y="15" fill="black" >
            Rectangle #2: With opacity </text>
            
            <rect x="100" y="30" width="300" height="100" 
            style="fill:rgb(121,0,121);stroke-width:3;stroke:rgb(0,0,0);
            stroke-opacity:0.5;opacity:0.5"> </rect>
         </g>
      </svg>
   
   </body>
</html>
```

### **Rectangle #3 : With Rounded Corner**

```html
<html>
   <title>SVG Rectangle</title>
   <body>
      
      <h1>Sample SVG Rectangle Image</h1>
      
      <svg width="570" height="200">
         <g>
            <text x="0" y="15" fill="black" >
            Rectangle #3: With Rounded Corner </text>
            
            <rect x="100" y="100" rx="10" ry="10" width="300" height="100" 
            style="fill:rgb(121,0,121);stroke-width:3;stroke:rgb(0,0,0);"></rect>
         </g>
      </svg>
   
   </body>
</html>
```