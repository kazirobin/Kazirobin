# SVG Polygon

`<polygon>` element is used to draw a closed shape consisting of connected straight lines.

Following is the syntax declaration of `<polygon>` element. We've shown main attributes only.

```html
<polygon
   points="list of points"  > 
</polygon>
```

## Attributes

1. `points` − List of points to make up a polygon.

### Polygon #1 : Without Opacity

```html
<html>
   <title>SVG Polygon</title>
   <body>
      
      <h1>Sample SVG Polygon Image</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="0" y="15" fill="black" >Polygon #1: Without opacity.</text>
            
            <polygon points="150,75 258,137.5 258,262.5 150,325 42,262.6 42,137.5"
            stroke="black" stroke-width="3" fill="rgb(121,0,121)"></polygon>
         </g> 
      </svg>
   
   </body>
</html>
```

### Polygon #2 : With Opacity

```html
<html>
   <title>SVG Polygon</title>
   <body>
      <h1>Sample SVG Polygon Image</h1>
      
      <svg width="800" height="800"> 
         <g>
            <text x="0" y="15" fill="black" >Polygon #2: With opacity </text>
         
            <polygon points="150,75 258,137.5 258,262.5 150,325 42,262.6 42,137.5"
            style="fill:rgb(121,0,121);stroke-width:3;
            stroke:rgb(0,0,0);stroke-opacity:0.5;opacity:0.5"></polygon>
         </g>
      </svg>
      
   </body>
</html>
```