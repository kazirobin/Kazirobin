# useLocation

`CreatedAt- 17 May 2024 / RevisedAt -` 

The `useLocation` hook in React Router is used to return the current location of a React component. The useLocation returns the current location as an object and comes with props such as `pathname`, `state`, `search`, `key`, `hash`

These props can be used with useEffect hook to perform side effects such as clicks onScroll or return state parsed to a Link component.

To use `useLocation` hook, import it from the `react-router-dom` as indicated below.

```jsx
import { useLocation } from 'react-router-dom';
```

Then create and store the `useLocation` hook to a `location` variable as indicated below.

```jsx
import { useLocation } from 'react-router-dom';

export default function App(){

const location = useLocation()

   retun(
     <><p>Hello, useLocation</p></>
   )

}
```

With the `location` variable, the `useLocation` props can be accessed. For example

```jsx
import { useLocation } from 'react-router-dom';

export default function App(){

const location = useLocation()

console.log(location)

retun(
 <><p>Hello, useLocation</p></>
 )
}
```

This should return the `location` variable as an object.

![1_ST5YxVCuJDzPS2PKG8zFyA.webp](useLocation%201b2aeacbb29981738335f6e85d04d3f4/1_ST5YxVCuJDzPS2PKG8zFyA.webp)

## pathname

The `pathname` property (prop) from the `location` object is used to return the path name of a given component. The path name is the name that comes after the port number.

```jsx
                    //pathname 
                         👇
http://localhost:5173/products
                  👆
            //port number
```

From the code sample, the `pathname` is the forward slash and the products text 👉 `/products`

Access the `pathname` as follows ;

```jsx
import { useLocation } from 'react-router-dom';

export default function App(){

 // Dot Notation
 const location = useLocation()
 👉 console.log(location.pathname)

// Object Destructuring 
 const {pathname} = useLocation()
 👉 console.log(pathname)
 
 retun(
 <><p>Hello, useLocation</p></>
 )
}
```

```jsx
// layouts/Navbar.js
<div className="main">
   {pathname !== "" ? (
   <aside>
     <Link to="#sectionFour" className="product-btn">
       Click Button
     </Link>
   </aside>
   ) : null}
</div>
```

Here, the `pathname` returns a button element when the user clicks.

## state

The `state` property (prop) from the `location` object is used to set data on parent components that can be accessed by the children components.

To set `state` on the parent component, parse the `state` property and assign it a value as specified below.

```jsx
<li>
 <NavLink
   to="/"
   state={`Welcome to the ${
   pathname.substring(1) !== "" ? "home" : ""
   } page`}
   >
   Home
   </NavLink>
   </li>
   …
   <li>
   <NavLink
   to="products"
   state={`Welcome to the ${pathname.substring(1)} page`}
   >
   Products
 </NavLink>
 </li>
```

Here, the `pathname` of the specific link the user clicks is returned as a string and we applied the following functions to the state props.

1. `substring(1)` This method removes the forward slash from the pathname

2. the ternary operator checks and returns “home” if the path contains an empty string.

## search

The `search` property (prop) from the `location` object is used to get the query string in a URL.

For example, take this URL `”*http://example.com/search?age=20&name=alex*";`

The query string refers to a portion in the URL starting from the `?` character followed by a key (’age’ and ‘name’ ) and value (’20’ and ‘alex’) pairs. These keys and value pairs are called parameters and are separated by the `&` character.

Access the `search` as follows ;

```jsx
import { useLocation } from 'react-router-dom';

export default function App(){
 
 // Dot Notation
 const location = useLocation()
 👉 console.log(location.search)
// Object Destructuring 
 const {search} = useLocation()
 👉 console.log(search)
 
 retun(
 <><p>Hello, useLocation</p></>
 )
}
```

## key

The `key` property (prop) from the `location` object is used to hold a unique identifier (id) from the current URL.

Access the `key` as follows ;

```jsx
export default function App(){
 
 // Dot Notation
 const location = useLocation()
 👉 console.log(location.key)
// Object Destructuring 
 const {key} = useLocation()
 👉 console.log(key)
 
 retun(
 <><p>Hello, useLocation</p></>
 )
}
```

```jsx
export default function Navbar() {
 const { pathname, key } = useLocation();
return (
 <>
 <ul>
 <li>
 <NavLink to="/">Home</NavLink>
 </li>
 …
 <li>
 <NavLink to="products">Products</NavLink>
 </li>
 </ul>
 
{/* Outlet */}
 <Outlet />
 <div className="main">
 {pathname !== "" ? (
 <aside>
 <Link className="product-btn">Click Button</Link>
 </aside>
 ) : null}
<p>
 the return text is a key: <i className="key">{key}</i>
 </p>
 </div>
 </>
 );
}
```

## hash

The `hash` property (prop) from the `location` object is used to set the current location in the `#` hash segment of the current URL.

This is useful in cases where you want to navigate between different sections on the same page or navigate to a specific section on another page.

Access the `hash` as follows ;

```jsx
export default function App(){
 
 // Dot Notation
 const location = useLocation()
 👉 console.log(location.hash)
// Object Destructuring 
 const {hash} = useLocation()
 👉 console.log(hash)
 
 retun(
 <><p>Hello, useLocation</p></>
 )
}
```