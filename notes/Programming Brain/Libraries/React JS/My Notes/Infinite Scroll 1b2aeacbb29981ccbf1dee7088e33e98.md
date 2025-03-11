# Infinite Scroll

Infinite scroll, also known as endless scrolling or continuous scrolling, is **a technique for loading and displaying content progressively as the user scrolls down a webpage or through a list or a feed of items**.

## What is Intersection Observer?

The Intersection Observer is a browser API that provides a way to asynchronously observe or detect visibility of two elements in relation to each other.

As per MDN, this API is mostly used for performing visibility related tasks which includes lazy-loading of images and implementing "infinite scrolling" web sites, where more and more content is loaded and rendered as you scroll.

## Implementing Infinite Scroll In JavaScript

The Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.

Historically, detecting visibility of an element, or the relative visibility of two elements in relation to each other, has been a difficult task for which solutions have been unreliable and prone to causing the browser and the sites the user is accessing to become sluggish. As the web has matured, the need for this kind of information has grown. Intersection information is needed for many reasons, such as:

- Lazy-loading of images or other content as a page is scrolled.
- Implementing "infinite scrolling" websites, where more and more content is loaded and rendered as you scroll, so that the user doesn't have to flip through pages.
- Reporting of visibility of advertisements in order to calculate ad revenues.
- Deciding whether or not to perform tasks or animation processes based on whether or not the user will see the result.

```jsx
const circle = document.getElementById("circle");

const observer = new IntersectionObserver((items) => {
  const trackingInfo = items[0];

  if (trackingInfo.isIntersecting) {
    console.log("Circle is visible");
    observer.disconnect();
  } else {
    console.log("Circle is not visible");
  }
});

observer.observe(circle);
```

## Implementing Infinite Scroll In React

For the infinite scrolling we will be using an open source [Dummy Products List](https://dummyjson.com/).

For basic project setup, I created a simple React project with Vite and added Tailwind CSS to it. Also, for calling APIs, I used browser fetch api

To do an infinite scroll, we need to increment page number count when last element of the list is visible to user. This will be done by intersection observer.

Our intersection observer will observe if the last element is visible or not, if it is, we will increment the page number by 1. As our useEffect will run on change in page number, the API will get called and hence we will get list of more products.

```jsx
import { useEffect } from "react";
import { useRef } from "react";
import { useState } from "react";
import Product from "./Product";

const productsPerPage = 6;

export default function ProductList() {
  const [products, setProducts] = useState([]);
  const [page, setPage] = useState(0);
  const [hasMore, setHasMore] = useState(true);

  const loaderRef = useRef(null);

  useEffect(() => {
    const fetchProducts = async () => {
      // Fetch product from mock api
      const response = await fetch(
        `https://dummyjson.com/products?limit=${productsPerPage}&skip=${
          page * productsPerPage
        }`
      );
      const data = await response.json();

      if (data.products.length === 0) {
        setHasMore(false);
      } else {
        setProducts((prevProducts) => [...prevProducts, ...data.products]);
        setPage((prevPage) => prevPage + 1);
      }
    };

    // Intersection observer callback
    const onIntersection = (items) => {
      const loaderItem = items[0];

      if (loaderItem.isIntersecting && hasMore) {
        fetchProducts();
      }
    };

    const observer = new IntersectionObserver(onIntersection);

    if (observer && loaderRef.current) {
      observer.observe(loaderRef.current);
    }

    // cleanup
    return () => {
      if (observer) observer.disconnect();
    };
  }, [hasMore, page]);

  return (
    <div>
      <div>
        {products.map((product) => (
          <Product key={product.id} product={product} />
        ))}
      </div>
      {hasMore && <div ref={loaderRef}>Loading products...</div>}
    </div>
  );
}

```