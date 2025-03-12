# Scroll Tracking In Next JS

This code snippet defines a custom React hook called useScroll. It uses the useEffect and useState hooks to manage state of scroll events based on certain conditions, such as top-left or left elements in an element's positioning

A custom React hook that provides the scroll position (X and Y) and direction.

```jsx
import { useEffect, useState } from "react";

export function useScroll() {
  const [lastScrollTop, setLastScrollTop] = useState(0);
  const [bodyOffset, setBodyOffset] = useState(
    typeof window !== "undefined"
      ? document.body.getBoundingClientRect()
      : { top: 0, left: 0 }
  );
  const [scrollY, setScrollY] = useState(bodyOffset.top);
  const [scrollX, setScrollX] = useState(bodyOffset.left);
  const [scrollDirection, setScrollDirection] = useState<"up" | "down">();

  const listener = (e: Event) => {
    if (typeof window !== "undefined") {
      setBodyOffset(document.body.getBoundingClientRect());
      setScrollY(-bodyOffset.top);
      setScrollX(bodyOffset.left);
      setScrollDirection(lastScrollTop > -bodyOffset.top ? "down" : "up");
      setLastScrollTop(-bodyOffset.top);
    }
  };

  useEffect(() => {
    window.addEventListener("scroll", listener);

    return () => {
      window.removeEventListener("scroll", listener);
    };
  });

  return {
    scrollY,
    scrollX,
    scrollDirection
  };
}
```