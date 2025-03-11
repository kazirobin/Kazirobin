# Lazy Loading

Lazy loading is one of the most common design patterns used in web and mobile development. It is widely used with frameworks like Angular and React to increase an application’s performance by reducing initial loading time.

In the earlier versions of React, lazy loading was implemented using third-party libraries. However, React introduced two new native features to implement lazy loading with the React v16.6 update.

In this article, I will discuss what lazy loading is, how to implement it with React, and its pros and cons.

## What Is Lazy Loading?

In simple terms, lazy loading is a design pattern. It allows you to load parts of your application on-demand to reduce the initial load time. For example, you can initially load the components and modules related to user login and registration. Then, you can load the rest of the components based on user navigation.

You might not feel much difference when using lazy loading for small-scale applications. But it significantly impacts large-scale applications by reducing the initial load time. Ultimately, it improves both the user experience and the application’s performance.

## Advantages of Lazy Loading

- Reduces initial loading time by reducing the bundle size.
- Reduces browser workload.
- Improves application performance in low bandwidth situations.
- Improves user experience at initial loading.
- Optimizes resource usage.

## Disadvantages of Lazy Loading

- Not suitable for small-scale applications.
- Placeholders can slow down quick scrolling.
- Requires additional communication with the server to fetch resources.
- Can affect SEO and ranking.

## Implementing Lazy Loading with React

Usually, lazy loading is not used in React applications, since we mostly use React to develop single-page applications. Developers can bundle the entire code as a single bundle and use it for deployments.

But, as the application gets complex, we need to consider performance and user experience. In such situations, we need to use the lazy-loading techniques available with React to bundle the critical and noncritical parts of the application separately.

You can use modern bundlers and transpilers like Webpack and Babel to implement applications following the modular pattern. Then, you can use code splitting to divide the application bundle into smaller ones and lazy load them.

React introduced two native features with the version 16.6 release to implement lazy loading in React applications. First, they use the power of code splitting and dynamic imports to allow developers to implement lazy loading for their applications easily.

So, let’s see how we can implement lazy loading in React.

## React.lazy()

**React.lazy()** allows developers to easily create components with dynamic imports and render them as normal components. When the component is rendered, it will automatically load the bundle that contains the rendered component.

You need to provide a single input parameter to call **React.lazy()**. It accepts a function as an input parameter, and that function should return a promise after loading the component using **import()**. Finally, the returned promise from **React.lazy()** will give you a module with a default export containing the React component.

The following code shows how to use the **React.lazy()** function.

```jsx
// Without React.lazy()
import AboutComponent from './AboutComponent ';

// With React.lazy()
const AboutComponent = React.lazy(() => import('./AboutComponent '));

const HomeComponent = () => (
    <div><AboutComponent /></div>
)
```

Here is a different dynamic pattern for Lazy Loading. First, create a utils folder in src with `importLazy` this function returns a promise that why when you use this it's mandatory with `async` function.

```jsx
import { lazy } from "react";

export default function importLazy(file) {
  return lazy(() => import(`../components/${file}`));
}
```

Now time to implement dynamic lazy loading.

```jsx
import importDemofrom "./utils/importDemo";

const loadDemo = async (file) => {
    const Component = await importDemo(file);
    return <Component />;
  };

  const selectDemo = async (file) => {
    const DemoComponent = await loadDemo(file);

    setSelectedDemo(DemoComponent);
  };
```

Component data should be like this:

```jsx
const demos = [
  {
    id: 1,
    name: "shape",
    file: "ShapeDemo",
  },
  {
    id: 2,
    name: "color",
    file: "ColorDemo",
  },
  {
    id: 3,
    name: "size",
    file: "SizeDemo",
  },
];

export default demos;

```

## React.Suspense

When we use lazy loading, components are rendered as we navigate. So, we need to have a placeholder for those components until they are loaded. As a solution, **React.Suspense** was introduced, and it acts as a wrapper for the lazy components.

You can wrap a single lazy component, multiple lazy components, or multiple lazy components with different hierarchy levels with **React.Suspense**. In addition, it accepts a prop named fallback as the placeholder, and you can pass a component or an element for that.

For example, you can pass the waiting or loading message as the **fallback** prop, and it will be displayed until the wrapped lazy component is rendered.

```jsx
import React, { Suspense } from "react";
const AboutComponent = React.lazy(() => import('./AboutComponent'));

const HomeComponent = () => (
    <div>
				<Suspense fallback = { <div> Please Wait... </div> } >
            <AboutComponent />
				</Suspense>
		</div>
);
```

As you can see, you need to use both the **React.lazy()** and **React.Suspense** features to build a lazy-loading component in React. These features are straightforward and anyone with basic React knowledge can easily use them.

However, sometimes you might face issues due to promise rejections in the **React.lazy()** function. To overcome such situations, you need to create a React error boundary component and wrap the Suspense components using it.

```jsx
import React, { Suspense } from "react";
import ErrorBoundary from "./error.boundary.js";
const AboutComponent = React.lazy(() => import('./AboutComponent'));

const HomeComponent = () => (
    <div>
			<ErrorBoundary>
        <Suspense fallback = { <div> Please Wait... </div>} >
          <AboutComponent />
				</Suspense>
			</ErrorBoundary>
    </div>
);
```

## Don’t Use Too Much Lazy Loading

As discussed, lazy loading has many benefits. But overusing it can have a significant negative impact on your applications. So, it is essential to understand when web developers should use lazy loading and when we should not.

You should not opt for lazy loading if your application has a small bundle size. There is no point in splitting a small bundle into pieces, and it will only increase coding and configuring effort.

Also, there are special application types like e-commerce sites that can be negative impacted by lazy loading. For example, users like to scroll through quickly when searching for items. If you lazy load shopping items, it will break the scrolling speed and result in a bad user experience. So, you should analyze the company’s website usage before using lazy loading.

On the other hand, lazy loading can be a real life-saver in large-scale projects. Projects with large bundle sizes take a significant amount of time for the initial load, and it is a significant drawback in terms of user experience. So, think of application requirements, scale, and current performance of the application before choosing lazy loading.