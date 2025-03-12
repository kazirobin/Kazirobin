# useLockBody

The useLockBodyScroll hook temporarily disables scrolling on the document body. This can be beneficial in scenarios where you want to restrict scrolling while displaying a modal, a dropdown menu, or any other component that requires the user’s focus. Once the component using this hook is unmounted or no longer needed, the hook returns a cleanup function that restores the original overflow style, ensuring that the scroll behavior is reverted to its previous state.

### 1. Example

```jsx
import * as React from "react";

// @see https://usehooks.com/useLockBodyScroll.
export function useLockBody() {
  React.useLayoutEffect(() => {
    const originalStyle = window.getComputedStyle(document.body).overflow;
    document.body.style.overflow = "hidden";
    return () => (document.body.style.overflow = originalStyle);
  }, []);
}
```

### 2. Example

```jsx
import * as React from "react";

export function useLockBody(modal) {
  React.useLayoutEffect(() => {
    if (modal) {
      document.documentElement.setAttribute('style', 'overflow: hidden');
    } else {
      document.documentElement.removeAttribute('style');
    }

    return () => {
      document.documentElement.removeAttribute('style');
    };
  }, [modal]);
}
```