# React Portal In Next JS

We'll use native React portal API to move any component outside of the root div. Later, we'll wrap it with a custom hook to avoid z-index problems.

---

```jsx
"use client";

import { useEffect, useRef } from "react";
import { createPortal } from "react-dom";

export default function usePortal() {
  const pathRef = useRef(null);

  useEffect(() => {
    const portalRoot = document.getElementById("portal-root");
    const divElement = document.createElement("div");
    portalRoot.appendChild(divElement);

    pathRef.current = divElement;

    // Cleanup function
    return () => {
      portalRoot.removeChild(divElement);
    };
  }, []);

  return (children) => createPortal(children, pathRef.current);
}
```