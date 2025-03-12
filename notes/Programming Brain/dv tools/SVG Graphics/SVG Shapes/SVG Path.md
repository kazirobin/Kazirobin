# SVG Path

`<path>` element is used to draw a connected straight lines.

Following is the syntax declaration of `<path>` element. We've shown main attributes only.

```html
<path
   d="data" >  
</path>
```

## Attributes

1. `d` − path data,usually a set of commands like moveto, lineto etc.
2. `M` − moveto − move from one point to another point.
3. `L` − lineto − create a line.
4. `H` − horizontal lineto − create a horizontal line.
5. `V` − vertical lineto − create a vertical line.
6. `C` − curveto − create a curve.
7. `S` − smooth curveto − create a smooth curve.
8. `Q` − quadratic Bezier curve − create a quadratic Bezier curve.
9. `T` − smooth quadratic Bezier curveto − create a smooth quadratic Bezier curve
10. `A` − elliptical Arc − create a elliptical arc.
11. `Z` − closepath − close the path.

`<path>` element is used to define any path. Path element uses Path data which comprises of number of commands. Commands behaves like a nip of pencil or a pointer is moving to draw a path.

As above commands are in Upper case, these represents absolute path. In case their lower case commands are used, then relative path is used.

### Path #1: Without Opacity

```html
<html>
   <title>SVG Path</title>
   <body>
   
      <h1>Sample SVG Path Image</h1>
      
      <svg width="570" height="320">
         <g>
            <text x="0" y="10" fill="black" >Path #1: Without opacity.</text>
            
            <path d="M 100 100 L 300 100 L 200 300 z" 
            stroke="black" stroke-width="3" fill="rgb(121,0,121)"> </path>
         </g> 
      </svg>
   
   </body>
</html>
```

### Path #1: With Opacity

```html
<html>
   <title>SVG Path</title>
   <body>
      
      <h1>Sample SVG Path Image</h1>
      
      <svg width="800" height="800"> 
         <g>
            <text x="0" y="15" fill="black" >Path #2: With opacity </text>
            
            <path d="M 100 100 L 300 100 L 200 300 z"
            style="fill:rgb(121,0,121);stroke-width:3;
            stroke:rgb(0,0,0);stroke-opacity:0.5;"> </path>
         </g>
      </svg>
   
   </body>
</html>
```