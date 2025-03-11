# useDeferredValue

`CreatedAt- 27 Feb 2024 / RevisedAt-` 

React 18 recently had its official non-beta release and with it came multiple new React hooks to help deal with concurrency and rendering slow content. One of those hooks is the `useDeferredValue` hook which is easy to use but difficult to understand. In this article I will help explain how this hook works so you can understand how and when to best use it.

## Why Do You Need useDeferredValue?

Before we can talk about what this hook does and how to use it we first need to understand a few concepts about how state and rerendering works in React in order to understand the use case for this hook.

Imagine you have the following code.

```jsx
function App() {
  const [name, setName] = useState("")
  const computedValue = useMemo(() => {
    return getComputedValue(name)
  }, [name])

  function handleChange(e) {
    setName(e.target.value)
  }

  return <input type="text" value={name} onChange={handleChange} />
}
```

This is a very simple component with one state variable and a `computedValue` which is derived from our state. When the value in the input is changed our name state is updated and then after that state finishes updating our entire component rerenders. During that rerender our `computedValue` is recalculated since the name value that we are memoizing on has changed.

Normally this isn’t a problem, but sometimes the code inside `useMemo` is slow to run or computationally expensive. In those cases this can lead to performance problems.

```jsx
function App() {
  const [name, setName] = useState("")
  const list = useMemo(() => {
    return largeList.filter(item => item.name.includes(name))
  }, [name])

  function handleChange(e) {
    setName(e.target.value)
  }

  return (
    <>
      <input type="text" value={name} onChange={handleChange} />
      {list.map(item => (
        <ListComponent key={item.id} item={item} />
      ))}
    </>
  )
}
```

In this example we are now using the name state variable to filter a large list of items. Our list is incredibly long so looping through the entire list, filtering each item, and rendering them all to the screen is quite time consuming and especially on older devices will be very slow to process. This is a problem since this list updates every time our name state changes. This delays our component rerender since on each keystroke of our input we need to do a massive filtering of this list which makes the UI sluggish to use. Below is an example of what this would look like.

Instead of rendering out thousands of items to the screen, I am instead emulating the slowness artificially and only rendering a few items to the screen so as to not overwhelm your computer. Also, the items being rendered are just exact copies of whatever you type in to the input field and you can only enter one character at a time into the input field or it will not work as expected.

Item: a
Item: a
Item: a
Item: a
Item: a

As you can see in this example when you try to type into the input box it is really slow and takes about a second to update the input box. This is because rendering and processing the list takes so long. This is where `useDeferredValue` comes in.

## useDeferredValue Explained

The `useDeferredValue` hook allows us to fix this slow render problem by implementing a delay before some information is calculated. This works in a very similar way to debouncing and throttling since our deferred value will only be calculated after the important state updates have finished running.

```jsx
function App() {
  const [name, setName] = useState("")
  const deferredName = useDeferredValue(name)
  const list = useMemo(() => {
    return largeList.filter(item => item.name.includes(deferredName))
  }, [deferredName])

  function handleChange(e) {
    setName(e.target.value)
  }

  return (
    <>
      <input type="text" value={name} onChange={handleChange} />
      {list.map(item => (
        <ListComponent key={item.id} item={item} />
      ))}
    </>
  )
}
```

In the above example we have fixed this issue by adding in the `useDeferredValue` hook. This hook takes a single parameter which is the value you want setup your throttle/debounce on. This hook will then return a value which will be the deferred version of the value you pass in. This means that when our `name` variable changes the `deferredName` will still stay the same since `useDeferredValue` will not immediately update the value of the `deferredName`. This allows time for our component to completely rerender with the new name value since our list will not try to update itself as it is waiting for the `deferredName` to change. This makes the app feel more responsive since the input will update immediately while the list will be delayed in its update.

The reason the list is delayed is because we changed our `useMemo` code to rely on the `deferredName` instead of the actual name. This means that if we change the name our `deferredName` will wait to update until after the UI has had time to update with the new name value in the input field. If we continue to change our input in a short period of time (for example by typing quickly in the input) the `deferredName` value will continue to stay unchanged and our list will not update. The only thing that will update is the name variable until there is a pause in the name value changing. Once we stop typing then React will update the `deferredName` value with the most recent `name` value and rerender the list.

Here is an example of what our list acts like with the `useDeferredValue` hook.

Item: a
Item: a
Item: a
Item: a
Item: a

You can see that our input updates immediately when you type, but the actual list itself does not update until later. The old value of our list continues to stay on the screen until there has been a delay long enough for it to render itself out to the screen.

Using this hook is quite easy, but this is not something you want to use all the time. You should only use this hook if you are having performance issues with your code and there are no other ways to fix those performance concerns. If you use this hook all the time you will actually make your app less performant since React will be forced to do extra rerenders of your app. This is because it will do the initial rerender and the deferred rerender when it could have done them both in one update without `useDeferredValue`.