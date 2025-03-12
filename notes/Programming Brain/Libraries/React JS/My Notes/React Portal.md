# React Portal

`CreatedAt- 28 Feb 2024 / RevisedAt-` 

React Portals are a powerful feature in React that allows you to render components outside the current React tree hierarchy. With portals, you can easily render elements into different parts of the DOM, such as modals, tooltips, or any other component that needs to break out of the component’s container.

## What are React Portals?

React Portals provide a way to render components into a DOM node outside the component hierarchy. Typically, when you render a component in React, it gets inserted into the DOM as a child of its parent component. However, there are scenarios where you might need to render a component at a different location in the DOM, such as when creating a modal or dropdown menu.

React Portals solve this problem by allowing you to render a component’s output to a different DOM node outside of its parent component’s DOM hierarchy. This enables you to create components that can be visually displayed at any location in the DOM while still maintaining their logical position in the component hierarchy.

Under the hood, React Portals use a feature called “portal” in `react-dom`. `react-dom` provides a method called `[createPortal](https://react.dev/reference/react-dom/createPortal#)` that takes two arguments: the first is the content you want to render, which is also referred to as children, and the second is the DOM node where you want to render it, as shown below:

```jsx
import {createPortal} from 'react-dom';
createPortal(children, domNode);
```

### Some use cases of React Portals include:

- **Modal dialogs**: modals typically overlay the entire page and require rendering outside the current component hierarchy to ensure that they appear on top of other content. React Portals allow you to easily render modal components outside of their parent components and manage their visibility and behavior.
- **Tooltips and popovers**: tooltip and popover components often need to be rendered close to a specific element or position on the page. React Portals enable you to render these components in a different part of the DOM, precisely positioned relative to the triggering element.
- **Dropdown menus**: dropdown menus require rendering a menu component outside the parent component to ensure that it appears correctly in terms of positioning and layering. React Portals make it convenient to render dropdown menus outside of the regular component hierarchy, while still maintaining their interaction with the triggering elements

## Benefits of using React Portals

React Portals offer several benefits when it comes to building React applications, some of which are:

- **Flexible Component Placement**: React Portals allow you to render components at any location in the DOM, even outside of the current component hierarchy. This provides greater flexibility in designing complex UIs and positioning components precisely where needed.
- **Separation of Concerns**: portals enable you to separate the visual representation of a component from its logical position in the component hierarchy. This separation improves code organization and makes understanding and maintaining your codebase easier.
- **Avoidance of CSS Conflicts**: by rendering components via portals, you can isolate their styles from their parent and sibling components. This reduces the likelihood of CSS conflicts and ensures that the styles of your portal components remain unaffected by the surrounding environment.
- **Enhanced Accessibility**: portals are especially useful for creating accessible components like modals. By rendering them at the top level of the DOM, screen readers and assistive technologies can access the content more easily, improving the overall accessibility of your application.
- **Integration with Third-Party Libraries**: React Portals facilitate the integration of third-party libraries or components that require rendering outside of the main React hierarchy. This enables the seamless incorporation of external functionalities while preserving the integrity of your React application.
- **Optimized Performance**: React Portals can help improve the performance of your application by minimizing unnecessary re-renders. Since portal components exist outside of the regular component hierarchy, they can be updated independently, preventing unnecessary updates to the entire application.

## How to use React Portals

To demonstrate how react portals work, let’s create a modal example.

### App component

We’ll create an app component to render a button element and a modal component. The modal will only be visible when we click on the button.

```jsx
import React, { useState } from 'react'
import './App.css';
import Modal from './Modal.jsx';
export default function App() {
 const [isOpen, setOpen]= useState(false)
 return (
   <div>
     <button onClick={()=> {setOpen(true)}}>show button</button>
     <Modal isOpen= {isOpen} onClose={()=>setOpen(false)}/>
   </div>
 )
};
```

The code above sets up an App component with a button that toggles the display of a modal component based on the state of the `isOpen` variable. Clicking the button shows the modal, and triggering the `onClose` function closes the modal by updating the state.

### Modal component

We’ll use `createPortal` inside of our modal component. Let’s create a file called `Modal.jsx` and paste this in:

```jsx
import React from 'react'
import {createPortal} from 'react-dom';
import './Modal.css';
export default function Modal({isOpen, onClose}) {
   if(!isOpen)return null;
 return createPortal(
   <div className='modal'>
       <div className='modal-container'>
           <div  className='modal-body'>
               <p>sample modal</p>
           </div>
           <button onClick={onClose}>Close</button>
       </div>
    
   </div>
   , document.getElementById('modal') // this will let react-dom know that we want to render this modal outside the current React tree
 )
}
```

The modal component receives two props: `isOpen` and `onClose`. The `isOpen` prop indicates whether the modal should be visible or hidden, while the `onClose` prop is a function to be called when the modal is closed.

If the `isOpen` prop is `false`, then the modal will not be displayed, and the component returns null, effectively rendering nothing.

When the `isOpen` prop is `true`, it executes the createPortal function. This function renders the modal content outside the current React component tree. It takes two parameters: the JSX code representing the modal component and the target DOM element where the modal should be rendered. In our case, the target DOM element is specified as `document.getElementById('modal')`. This instructs `react-dom` to render the modal in the DOM element with the `modal` id, effectively placing it outside the regular React component hierarchy.