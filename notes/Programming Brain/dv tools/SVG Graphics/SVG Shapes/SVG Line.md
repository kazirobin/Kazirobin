# SVG Line

`<line>` element is used to draw line with a start point and end point.

Following is the syntax declaration of `<line>` element. We've shown main attributes only.

```html
<line
   x1="x-axis co-ordinate"
   y1="y-axis co-ordinate"
   
   x2="x-axis co-ordinate" 
   y2="y-axis co-ordinate" >    
</line>
```

## Attributes

1. `x1` − x-axis co-ordinate of the start point. Default is 0.
2. `y1` − y-axis co-ordinate of the start point. Default is 0.
3. `x2` − x-axis co-ordinate of the end point. Default is 0.
4. `y2` − y-axis co-ordinate of the end point. Default is 0.

### Line #1 : Without Opacity

```html
<html>
   <title>SVG Line</title>
   <body>
      
      <h1>Sample SVG Line Image</h1>
      
      <svg width="800" height="800">
         <g>
            <text x="0" y="15" fill="black" >Line #1: Without opacity.</text>
            
            <line x1="20" y1="20" x2="150" y2="150" 
            stroke="black" stroke-width="3" fill="rgb(121,0,121)"></line> 
         </g> 
      </svg>
   
   </body>
</html>
```

### Line #2: With Opacity

```html
<html>
   <title>SVG Line</title>
   <body>
      
      <h1>Sam>le SVG Line Image</h1>
      
      <svg width="800" height="800"> 
         <g>
            <text x="0" y="15" fill="black" >Line #2: With opacity </text>
            
            <line x1="20" y1="20" x2="150" y2="150"  
            style="fill:rgb(121,0,121);stroke-width:3;
            stroke:rgb(0,0,0);stroke-opacity:0.5;opacity:0.5"></line> 
         </g>
      </svg>
   
   </body>
</html>
```