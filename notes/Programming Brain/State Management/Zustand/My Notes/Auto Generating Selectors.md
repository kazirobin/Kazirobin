# Auto Generating Selectors

We recommend using selectors when using either the properties or actions from the store. You can access values from the store like so:

```jsx
const bears = useBearStore((state) => state.bears)
```

However, writing these could be tedious. If that is the case for you, you can auto-generate your selectors.

## Create the following function: `createSelectors`

Create a file named liked `./src/lib/utils.ts`

```jsx
import { StoreApi, UseBoundStore } from 'zustand'

type WithSelectors<S> = S extends { getState: () => infer T }
  ? S & { use: { [K in keyof T]: () => T[K] } }
  : never

export const createSelectors = <S extends UseBoundStore<StoreApi<object>>>(
  _store: S,
) => {
  let store = _store as WithSelectors<typeof _store>
  store.use = {}
  for (let k of Object.keys(store.getState())) {
    ;(store.use as any)[k] = () => store((s) => s[k as keyof typeof s])
  }

  return store
}
```

If you have a store like this:

```jsx
interface BearState {
  bears: number
  increase: (by: number) => void
  increment: () => void
}

const bearStore = create<BearState>((set) => ({
  bears: 0,
  increase: (by) => set((state) => ({ bears: state.bears + by })),
  increment: () => set((state) => ({ bears: state.bears + 1 })),
}))
```

Apply that function to your store:

```jsx
export const useBearStore = createSelectors(bearStore)
```

Now the selectors are auto generated and you can access them directly:

```jsx
// get the property
const bears = useBearStore.use.bears()

// get the action
const increment = useBearStore.use.increment()
```