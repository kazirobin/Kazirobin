# SVG Stroke

In Scalable Vector Graphics (SVG), the stroke attribute **defines the color or paint server used to draw the outline of an SVG shape**

SVG supports multiple stroke properties.

Following are the main stroke properties used.

1. `stroke` − defines color of text, line or outline of any element.
2. `stroke-width` − defines thickness of text, line or outline of any element.
3. `stroke-linecap` − defines different types of ending of a line or outline of any path.
4. `stroke-dasharray` − used to create dashed lines.

### Stroke #1 : Example

```html
<html>
   <title>SVG Stroke</title>
   <body>
   
      <h1>Sample SVG Stroke</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="30" y="30" >Using stroke: </text>
            <path stroke="red" d="M 50 50 L 300 50" />
            <path stroke="green" d="M 50 70 L 300 70" />
            <path stroke="blue" d="M 50 90 L 300 90" />
         </g> 
      </svg>
   
   </body>
</html>
```

### Stroke #2 : **Stroke Width**

```html
<html>
   <title>SVG Stroke</title>
   <body>
      
      <h1>Sample SVG Stroke</h1>
      
      <svg width="800" height="800">
         <text x="30" y="10" >Using stroke-width: </text>
         <path stroke-width="2" stroke="black" d="M 50 50 L 300 50" />
         <path stroke-width="4" stroke="black" d="M 50 70 L 300 70" />
         <path stroke-width="6" stroke="black" d="M 50 90 L 300 90" />
      </svg>
      
   </body>
</html>
```

### Stroke #3 : S**troke Linecap**

```html
<html>
   <title>SVG Stroke</title>
   <body>
      
      <h1>Sample SVG Stroke</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="30" y="30" >Using stroke-linecap: </text>
         
            <path stroke-linecap="butt" stroke-width="6" 
            stroke="black" d="M 50 50 L 300 50" />
         
            <path stroke-linecap="round" stroke-width="6" 
            stroke="black" d="M 50 70 L 300 70" />
         
            <path stroke-linecap="square" stroke-width="6"
            stroke="black" d="M 50 90 L 300 90" />
         </g>
      </svg>
   
   </body>
</html>
```

### Stroke #4 : S**troke Dasharray**

```html
<html>
   <title>SVG Stroke</title>
   <body>
   
      <h1>Sample SVG Stroke</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="30" y="30" >Using stroke-dasharray: </text>
            
            <path stroke-dasharray="5,5" stroke-width="6" 
            stroke="black" d="M 50 50 L 300 50" />
            
            <path stroke-dasharray="10,10" stroke-width="6" 
            stroke="black" d="M 50 70 L 300 70" />
            
            <path stroke-dasharray="20,10,5,5,5,10" stroke-width="6" 
            stroke="black" d="M 50 90 L 300 90" />
         </g>
      </svg>
   
   </body>
</html>
```