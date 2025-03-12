# SVG Linking

`<a>` element is used to create hyperlink. `"xlink:href"` attribute is used to pass the IRI (Internationalized Resource Identifiers) which is complementary to URI (Uniform Resource Identifiers).

Following is the syntax declaration of **<a>** element. We've shown main attributes only.

```html
<a
   xlink:show = "new" | "replace"
   xlink:actuate = "onRequest"
   xlink:href = "<IRI>"
   target = "_replace" | "_self" | "_parent" | "_top" | "_blank" | "<XML-Name>" >
</a>
```

## Attributes

1. `xlink:show` − for documentation purpose for XLink aware processors. Default is new.
2. `xlink:actuate` − for documentation purpose for XLink aware processors.
3. **`xlink:href**` − location of the referenced object.
4. `target` − used when targets for the ending resource are possible.

### Link #1 : Example

```html
<html>
   <title>SVG Linking</title>
   <body>
   
      <h1>Sample Link</h1>
      
      <svg width="800" height="800">
         <g>
            <a xlink:href="http://www.tutorialspoint.com"> 
               <text x="0" y="15" fill="black" >
               Click me to load TutorialsPoint DOT COM.</text>
            </a>
         </g> 
         
         <g>
            <text x="0" y="65" fill="black" >
            Click in the rectangle to load TutorialsPoint DOT COM</text>
            
            <a xlink:href="http://www.tutorialspoint.com"> 
               <rect x="100" y="80" width="300" height="100"
               style="fill:rgb(121,0,121);stroke-width:3;stroke:rgb(0,0,0)" /> 
            </a>
         </g>
      </svg>
   
   </body>
</html>
```