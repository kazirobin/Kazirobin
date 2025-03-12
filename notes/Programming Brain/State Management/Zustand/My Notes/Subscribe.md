# Subscribe

In Zustand, a popular state management library for React, `subscribe` is a method that allows you to listen for changes to the state in a store. You can use `subscribe` to handle side effects or perform actions based on state changes without causing re-renders. 

### For example of Bear Store

```jsx
import { create } from "zustand";
import type { StateCreator } from "zustand";

interface BearStoreState {
  bears: number;
  increase: () => void;
}

const bearStore: StateCreator<BearStoreState> = (set) => ({
  bears: 0,
  increase: () => set((state) => ({ bears: state.bears + 1 })),
});

export const useBearStore = create(bearStore);
```

### For example of  Counter Store

```jsx
import { useCounterStore } from "@/store/counter-store";

export default function Counter() {
  const { count, increment, decrement } = useCounterStore((state) => state);

  return (
    <div>
      <h1>Counter: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
}
```

### For example of  Bear Component

```jsx
import { useBearStore } from "@/store/bear-store";
import { useCounterStore } from "@/store/counter-store";
import { useEffect, useState } from "react";

export default function Bear() {
  const [isDisabled, setIsDisabled] = useState<number>(0);
  const { bears, increase } = useBearStore((state) => state);

  useEffect(() => {
    const unSub = useCounterStore.subscribe((state, prevState) => {
      if (prevState.count <= 5 && state.count > 5) {
        setIsDisabled(state.count);
      }
      console.log("Counter state changed", state, prevState);
    });

    return unSub;
  }, []);

  return (
    <div>
      <h1>Bears: {bears}</h1>
      <button disabled={isDisabled >= 5} onClick={increase}>
        Increase
      </button>
      {Math.random()}
    </div>
  );
}
```

### For example of  Counter Component

```jsx
import { useCounterStore } from "@/store/counter-store";

export default function Counter() {
  const { count, increment, decrement } = useCounterStore((state) => state);

  return (
    <div>
      <h1>Counter: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
}
```