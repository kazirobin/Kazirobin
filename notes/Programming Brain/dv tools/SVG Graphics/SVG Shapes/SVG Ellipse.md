# SVG Ellipse

`<ellipse>` element is used to draw ellipse with a center point and given two radii.

Following is the syntax declaration of **<ellipse>** element. We've shown main attributes only.

```html
<ellipse
   cx="x-axis co-ordinate"
   cy="y-axis co-ordinate"
   
   rx="length" 
   ry="length" >    
</ellipse>
```

## Attributes

1. `cx` − x-axis co-ordinate of the center of the ellipse. Default is 0.
2. `cy` − y-axis co-ordinate of the center of the ellipse. Default is 0.
3. `rx` − x-axis radius of the ellipse.
4. `ry` − y-axis radius of the ellipse.

### Ellipse #1: Without Opacity

```html
<html>
   <title>SVG Ellipse</title>
   <body>
   
      <h1>Sample SVG Ellipse Image</h1>
      <svg width="800" height="800">
         <g>
            <text x="0" y="15" fill="black" >Ellipse #1: Without opacity.</text>
            
            <ellipse cx="100" cy="100" rx="90" ry="50" 
            stroke="black" stroke-width="3" fill="rgb(121,0,121)"></ellipse>
         </g> 
      </svg>
   
   </body>
</html>
```

### Ellipse #2: With Opacity

```html
<html>
   <title>SVG Ellipse</title>
   <body>
      
      <h1>Sample SVG Ellipse Image</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="0" y="15" fill="black" >Ellipse #2: With opacity </text>
            
            <ellipse cx="100" cy="100" rx="90" ry="50" 
            style="fill:rgb(121,0,121);stroke-width:3;
            stroke:rgb(0,0,0);stroke-opacity:0.5;opacity:0.5"></ellipse> 
         </g>
      </svg>
   
   </body>
</html>
```