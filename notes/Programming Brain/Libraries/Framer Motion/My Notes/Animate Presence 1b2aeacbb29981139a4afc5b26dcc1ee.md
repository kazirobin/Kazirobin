# Animate Presence

`AnimatePresence` is the key component for easily animating the route transitions. It's job is to determine whether a component is mounting or unmounting and play an animation on our `<motion />` components. The routes we want to animate are within the `<Routes/>` component will mount and unmount but we also need to tell `AnimatePresence` if we want to animate at all, this is where the key prop comes in. We don't want to trigger an animation when we navigate to the same route, using the `ocation.pathname` as the key results in an animation which only triggers when we change to a new route.

```jsx
import { Route, Routes, useLocation } from "react-router-dom";
import Home from "./components/Home";
import About from "./components/About";
import { AnimatePresence } from "framer-motion";

export default function App() {
  const location = useLocation();
  const locationArr = location.pathname?.split("/") ?? [];

  return (
    <AnimatePresence mode="wait">
      <Routes location={location} key={locationArr[1]}>
        <Route path="/home" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </AnimatePresence>
  );
}
```

Now framer motion has checked the `exit` property in your individual `route` when you change a `route`. And you have already set the `exit` property framer motion automatically trigger you `motion div`.

```jsx
import { motion } from "framer-motion";
import { NavLink } from "react-router-dom";

export default function Home() {
  return (
    <motion.div
      initial={{ opacity: 0, scale: 0.5 }}
      animate={{ opacity: 1, scale: 1 }}
      transition={{ duration: 1 }}
      exit={{
        y: "-100vh",
        transition: {
          ease: "easeInOut",
        },
      }}
      className="grid w-full h-screen place-items-center"
    >
      <button className="px-5 py-1 bg-blue-600 border rounded-full">
        Home Page
      </button>
      <NavLink to="/about">Go About</NavLink>
    </motion.div>
  );
}
```

**Note:** Change route using `NavLink` that's come from `react-router-dom`. Because it does not work manually change the route url.

```jsx
import { NavLink } from "react-router-dom";
<NavLink to="/about">Go About</NavLink>
```