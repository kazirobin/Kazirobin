# React Portal

We'll use native React portal API to move any component outside of the root div. Later, we'll wrap it with a custom hook to avoid z-index problems.

---

```jsx
import { useEffect, useRef } from "react";
import { createPortal } from "react-dom";

export default function usePortal() {
  const domNode = document.getElementById("portal-root");
  const portalRef = useRef(null);

  // Check is portalRef null and document undefined
  if (portalRef.current === null && typeof document !== "undefined") {
    const elementDiv = document.createElement("div");
    portalRef.current = elementDiv;
  }

  useEffect(() => {
    const wrapper = portalRef.current;

    if (!wrapper || typeof document === "undefined") {
      return;
    }

    domNode.appendChild(wrapper);

    // Cleanup
    return () => {
      domNode.removeChild(wrapper);
    };
  }, []);

  return (children) =>
    portalRef.current && createPortal(children, portalRef.current);
}
```