# React Virtualized

A common requirement in web applications is displaying lists of data. Or tables with headers and scrolls. You have probably done it hundreds of times.

But what if you need to show thousands of rows at the same time?

And what if the pagination technique is not an option (or maybe it is but you still have to show a lot of information)? The infinite scrolling technique only limits rendering future elements and renders all previous rows, causing performance issues for very large lists.

First, you’ll see the problems with rendering a huge data set. Then, you’ll learn how React Virtualized solves those problems and how to efficiently render the list of the first example using the List and Autosizer components.

## Why use react-virtualized?

React developers typically use the `map` function and render lists with multiple rows. If they use that approach for rendering thousands of rows, the web browser will always create thousands of DOM elements even though a scrollbar typically hides overflowing content. Rendering a new DOM element needs physical memory and consumes CPU and GPU hardware when DOM element positions get changed with user events, such as scrolling. So, if we directly render large lists in web apps, the browser heavily uses the computer memory and increases CPU/GPU usage while rendering (especially with initial rendering phases).

![directly-rendered-large-list-reduces-react-performance-1.gif](React%20Virtualized%201b2aeacbb299813fa0a7e0cfbc5dea21/directly-rendered-large-list-reduces-react-performance-1.gif)

In less powerful devices or with more complex layouts, this could freeze the UI or even crash the browser, affecting app usability.

So how can we display thousands of rows in an efficient way?

One way is by using a library like react-virtualized, which renders large lists in a performance-friendly technique called virtual rendering. This library typically renders only visible rows in a large list and creates fewer DOM elements to reduce the performance overhead in apps. In other words, this library presents only the required rows and indicates the presence of other hidden rows virtually via CSS styles.

## How does react-virtualized work?

The main concept behind virtual rendering is rendering only what is visible.

There are 1,000 comments in the app, but it only shows around ten at any moment (the ones that fit on the screen), until you scroll to show more.

So it makes sense to load only the elements that are visible and unload them when they are not by replacing them with new ones.

react-virtualized implements virtual rendering with a set of components that basically work in the following way:

- They calculate which items are visible inside the area where the list is displayed (the viewport) based on the scrollbar positions and the viewport size
- They use a container (`div`) with relative positioning to absolute position the children elements inside of it by controlling its top, left, width, and height style properties

The above implementation strategy helps render large lists efficiently by rendering only elements that need to be presented to the user. For example, if you render a list of 10,000 movies with react-virtualized, it won’t create 10,000 DOM nodes instantly. Instead, it will indicate that you have many movies with a small-sized scrollbar and render a few (maybe 10 or 20) DOM nodes for visible movies when the user scrolls. Unlike the infinite scroll strategy, this implementation doesn’t keep past DOM elements in the DOM tree when the user scrolls down.

The react-virtualized library offers five main components:

- [Grid](https://github.com/bvaughn/react-virtualized/blob/master/docs/Grid.md): Renders tabular data along the vertical and horizontal axes
- [List](https://github.com/bvaughn/react-virtualized/blob/master/docs/List.md): Renders a list of elements using a `Grid` component internally
- [Table](https://github.com/bvaughn/react-virtualized/blob/master/docs/Table.md): Renders a table with a fixed header and vertically scrollable body content. It also uses a `Grid` component internally
- [Masonry](https://github.com/bvaughn/react-virtualized/blob/master/docs/Masonry.md): Renders dynamically-sized, user-positioned cells with vertical scrolling support
- [Collection](https://github.com/bvaughn/react-virtualized/blob/master/docs/Collection.md): Renders arbitrarily positioned and overlapping data

These components extend from React.PureComponent, which means that when comparing objects, it only compares their references to increase performance. You can read more about this here.

### On the other hand, react-virtualized also includes some HOC components:

- [ArrowKeyStepper](https://github.com/bvaughn/react-virtualized/blob/master/docs/ArrowKeyStepper.md): Decorates another component so it can respond to arrow-key events
- [AutoSizer](https://github.com/bvaughn/react-virtualized/blob/master/docs/AutoSizer.md): Automatically adjusts the width and height of another component
- [CellMeasurer](https://github.com/bvaughn/react-virtualized/blob/master/docs/CellMeasurer.md): Automatically measures a cell’s contents by temporarily rendering it in a way that is not visible to the user
- [ColumnSizer](https://github.com/bvaughn/react-virtualized/blob/master/docs/ColumnSizer.md): Calculates column-widths for grid cells
- [InfiniteLoader](https://github.com/bvaughn/react-virtualized/blob/master/docs/InfiniteLoader.md): Manages the fetching of data as a user scrolls a list, table, or grid
- [MultiGrid](https://github.com/bvaughn/react-virtualized/blob/master/docs/MultiGrid.md): Decorates a `Grid` component to add fixed columns and/or rows
- [ScrollSync](https://github.com/bvaughn/react-virtualized/blob/master/docs/ScrollSync.md): Synchronizes scrolling between two or more components
- [WindowScroller](https://github.com/bvaughn/react-virtualized/blob/master/docs/WindowScroller.md): Enables a `Table` or `List` component to be scrolled based on the window’s scroll positions

Now let’s see how to use the `List` component to virtualize the 5,000 comments example.

## Virtualizing a list

First, create a new React project:

```bash
npm create vite@latest
```

Install dependencies as follows:

```bash
npm install react-virtualized lorem-ipsum
```

Next, in `src/App.js`, import the `List` component from react-virtualized and do all necessary setups:

```jsx
import './App.css';

import { loremIpsum } from 'lorem-ipsum';
import { List } from 'react-virtualized';

const rowCount = 5000;
const listHeight = 400;
const rowHeight = 50;
const rowWidth = 700;

const list = Array(rowCount).fill().map((val, idx) => {
  return {
    id: idx,
    name: 'John Doe',
    image: 'http://via.placeholder.com/40',
    text: loremIpsum({
      count: 1,
      units: 'sentences',
      sentenceLowerBound: 4,
      sentenceUpperBound: 8
    })
  }
});
```

Let’s use the `List` component to render the list in a virtualized way. Add the following code after the above setup:

```jsx
function renderRow({ index, key, style }) {
  return (
    <div key={key} style={style} className="row">
      <div className="image">
        <img src={list[index].image} alt="" />
      </div>
      <div className="content">
        <div>{list[index].name}</div>
        <div>{list[index].text}</div>
      </div>
    </div>
  );
}

function App() {
  return (
    <div className="App">
      <div className="list">
        <List
          width={rowWidth}
          height={listHeight}
          rowHeight={rowHeight}
          rowRenderer={renderRow}
          rowCount={list.length}
          overscanRowCount={3} />
      </div>
    </div>
  );
}

export default App;
```

Then, add the following styling definitions to `src/App.css`:

```css
.App {
  text-align: center;
}

.list {
  padding: 10px;
}

.row {
  border-bottom: 1px solid #ebeced;
  text-align: left;
  margin: 5px 0;
  display: flex;
  align-items: center;
}

.image {
  margin-right: 10px;
}

.content {
  padding: 10px;
}
```

Notice two things.

First, the `List` component requires you to specify the width and height of the list. It also needs the height of the rows so it can calculate which rows are going to be visible.

Second, the component needs the number of rows (the list length) and a function to render each row. It doesn’t take the list directly.

For this reason, the implementation of the `renderRow` method needs to change.

This method won’t receive an object of the list as an argument anymore. Instead, the `List` component will pass it an object with the following properties:

We’ve implemented the `renderRow` function as follows:

```jsx
function renderRow({ index, key, style }) {
  return (
    <div key={key} style={style} className="row">
      <div className="image">
        <img src={list[index].image} alt="" />
      </div>
      <div className="content">
        <div>{list[index].name}</div>
        <div>{list[index].text}</div>
      </div>
    </div>
  );
}
```

**Note:** how the `index` property is used to access the element of the list that corresponds to the row that is being rendered. Also, make sure to add the incoming style to the `div` element to position rows correctly during scrolling (the library dynamically applies the CSS `top` property in this case).

If you run the app, you’ll see something like this:

![using-virtualized-list-rendering-large-list.gif](React%20Virtualized%201b2aeacbb299813fa0a7e0cfbc5dea21/using-virtualized-list-rendering-large-list.gif)

If you repeat the frame rate test, this time you’ll see a constant rate of 59/60 fps, low RAM usage, and no CPU/GPU usage spikes. If we look at the elements of the page in the developer tools tab, you’ll see that now the rows are placed inside two additional `div` elements:

[rows-places-inside-two-div-elements.avif](React%20Virtualized%201b2aeacbb299813fa0a7e0cfbc5dea21/rows-places-inside-two-div-elements.avif)

The number of additional elements is controlled with the [`overscanRowCount`](https://github.com/bvaughn/react-virtualized/blob/master/docs/overscanUsage.md) property. For example, if I set `3` as the value of this property:

```jsx
<List
  width={rowWidth}
  height={listHeight}
  rowHeight={rowHeight}
  rowRenderer={renderRow}
  rowCount={list.length}
  overscanRowCount={3} />
```

The number of elements I’ll see in the Elements tab will be around twelve.

Also, take a look at how the elements and their `top` style is updated dynamically:

![scrolling-events-change-css-top-attribute.gif](React%20Virtualized%201b2aeacbb299813fa0a7e0cfbc5dea21/scrolling-events-change-css-top-attribute.gif)

The downside is that you have to specify the width and height of the list as well as the height of the row. Luckily, you can use the `AutoSizer` and `CellMeasurer` components to solve this.

Let’s start with `AutoSizer`.

## Autoresizing a virtualized list

Components like `AutoSizer` use a pattern named function as child components.

As the name implies, instead of passing a component as a child:

```jsx
<AutoSizer>
  <List
  ...
  />
</AutoSizer>
```

You have to pass a function. In this case, one that receives the calculated width and height:

```jsx
<AutoSizer>
  {
    ({ width, height }) => {}
  }
</AutoSizer>
```

This way, the function will return the `List` component configured with the width and height:

```jsx
<AutoSizer>
  {
    ({ width, height }) => (<List
        width={width}
        height={height}
        rowHeight={rowHeight}
        rowRenderer={renderRow}
        rowCount={list.length}
        overscanRowCount={3} />
    )
  }
</AutoSizer>
```

The `AutoSizer` component will fill all of the available space of its parent so if you want to fill all the space after the header, in `src/App.css`, you can add the following line to the list class:

```css
.list {
  /*...*/
  height: calc(100vh - 20px);
}
```

### NOTE: If you are using Vite React project so that why you need some configuration.

First install `'esbuild-plugin-react-virtualized'`

```bash
npm i esbuild-plugin-react-virtualized
```

Second config Vite.config.js file

```jsx
// vite.config.js
import { defineConfig } from 'vite'
import fixReactVirtualized from 'esbuild-plugin-react-virtualized'

export default defineConfig({
  optimizeDeps: {
    esbuildOptions: {
      plugins: [fixReactVirtualized],
    },
  },
})
```