# Document Object Model

`CreatedAt- 24 Jan 2024 / RevisedAt-`

DOM stands for ‘Document Object Model’. In simple terms, it is a structured representation of the HTML elements that are present in a webpage or web app. DOM represents the entire UI of your application. The DOM is represented as a tree data structure. It contains a node for each UI element present in the web document. It is very useful as it allows web developers to modify content through JavaScript, also it being in structured format helps a lot as we can choose specific targets and all the code becomes much easier to work with.

---

## What Is Real DOM?

DOM stands for `Document Object Model` it is the structural representation of the HTML Document. Real DOM is the actual structure represented in the User Interface while Virtual DOM is the memory representation of the same. It is a tree-like Structure consisting of all nodes in an HTML document DOM represents the Ul of your applications.

## What Is Virtual DOM?

React JS Virtual DOM is an in-memory representation of the DOM. DOM refers to the `Document Object Model` that represents the content of XML or HTML documents as a tree structure so that the programs can be read, accessed and changed in the document structure, style, and content.

## How Rendering Process Work In A Browser

The work of the rendering engine starts once the user has requested a particular web page. The rendering engine starts receiving the Html, CSS and js files of the requested web page, through the networking layer. After receiving the content of the requested page, the following flow of the rendering engine begins:

![real-dom.jpg](Document%20Object%20Model%201b2aeacbb29981c28627f435c942ed91/real-dom.jpg)

- The requested HTML and CSS files of the requested page are parsed in chunks. Dom nodes are created to form the Dom tree and CSSOM tree.
- The render tree is constructed by combining the Dom and CSSOM Tree. The render tree contains both information about the order of the elements and their styling information. The render tree ensures that the content is displayed in the expected format.
- At this stage, every node is assigned with dedicated coordinates. To ensure that every element appears in the same position on the screen, this process is called the rendering process.
- In this stage, the render tree is traversed and every node as mentioned in the tree is painted on the screen.

## Is Real DOM Really Slow?

It is probably a bit of a misconception here. The DOM itself is not slow, however, when you make changes that trigger re-painting of the layout, that's where things start to slow down (especially if you do a lot of manipulation at once).

When we interact with `DOM`. Then the following(marked) process is done again. That's why some say Real Dom is slow.

Before, websites were multipaged. Now, we aim to accomplish numerous tasks and interact with content on a single page without the need for page refreshing. When a page is refreshed, the painting process is repeated, causing significant slowdown. This is where `React` comes in to address this issue.

![slow-real-dom.jpg](Document%20Object%20Model%201b2aeacbb29981c28627f435c942ed91/slow-real-dom.jpg)

## What Can We Do Now?

So we can optimize this process, consider the following techniques:

### 1. Batch Update

React uses something called batch updates to update the real DOM. It just means that the changes to the real DOM are sent in batches instead of sending any update for a single change in the state of a component.

### 2. Less DOM Operation

To reduce DOM access and improve performance, it is best to cache references to elements in variables and reuse them instead of querying the DOM again. Additionally, use document fragments to create and append multiple elements in one batch instead of one by one.

```jsx
// Batch Update -- fast

const container = document.querySelector(".container");

let array = [];
increment = 0;

while (increment < 10000) {
  array.push(++increment);
}

// this is fast because the dom is renedered only once
container.innerHTML = array.join(" ");

/*
// Individual Update -- slow

while (increment < 10000) {
    increment++;
    // everytime we are rendering the dom
    container.innerHTML += " " + increment;
}
*/

```

## How Does Virtual DOM Works?

Virtual DOM is a programming concept where a virtual representation of a UI is kept in memory synced with “Real DOM ” by a library such as `ReactDOM` and this process is called reconciliation. Virtual DOM makes the performance faster, not because the processing itself is done in less time.

- React thinks of its components as a tree-like structure.
    
    ![1.jpg](Document%20Object%20Model%201b2aeacbb29981c28627f435c942ed91/1.jpg)
    

- When there is a change in `C` Component, React immediately copies the actual `DOM` and creates a `Virtual DOM`.
    
    ![2.jpg](Document%20Object%20Model%201b2aeacbb29981c28627f435c942ed91/2.jpg)
    

- React re-renders component `C` and its child components.

![3.jpg](Document%20Object%20Model%201b2aeacbb29981c28627f435c942ed91/3.jpg)

- Now, React compares the previous `DOM` with the `Current DOM` using the `Diffing/Reconciliation` algorithm to identify any changes. If changes are detected in the `H` Element, React will then only modify the `H` Element.
    
    ![4.jpg](Document%20Object%20Model%201b2aeacbb29981c28627f435c942ed91/4.jpg)
    

- This process is relatively slow, but it is still much faster than repainting the actual DOM. It can be considered "Fast Enough.”