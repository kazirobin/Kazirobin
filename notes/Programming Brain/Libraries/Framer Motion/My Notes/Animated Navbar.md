# Animated Navbar

We’ll build a simple Navigation component, and we’ll see how we can create timing relationships between parent and children motion components.

## All Components

- `App.js`: this holds the heading texts.
- `Styles.js`: create, style, and export the motion components. The components are styled using styled-components.

Let’s take a look at the `App.js` file.

```jsx
import { Header, Nav, Link, SvgBox } from "./Styles";

function App() {
  const [isOpen, setIsOpen] = useState(false);
  const iconVariants = {
    opened: {
      rotate: 135
    },
    closed: {
      rotate: 0
    }
  };
  const menuVariants = {
    opened: {
      top: 0,
      transition: {
        when: "beforeChildren",
        staggerChildren: 0.5
      }
    },
    closed: {
      top: "-90vh"
    }
  };
  const linkVariants = {
    opened: {
      opacity: 1,
      y: 50
    },
    closed: {
      opacity: 0,
      y: 0
    }
  };

```

We create an `isOpen` state that will be used to check if the Navbar is open or not. We create 3 variant objects, `iconVariants`, `menuVariants`, and `linkVariants` where we define the animations for the `SvgBox`, `Nav`, and `Link` motion components respectively. The `iconVariants` is used to rotate the `SvgBox` 135deg when it’s hovered over. We don’t need to add “deg” to the value. In the `menuVariants`, we control the top position of the `Nav` like you would using the `position` property in CSS. We toggle the top position of the `Nav` based on the `isOpen` state.

With variants, we can create timing relationships between parent and children motion components. We define the relationship between parent `Nav` and its child, `Link` using the `when` property in the transition object. Here, set it to `beforeChildren`, so the parent component’s animations will finish before the child’s animation begins.

Using the `staggerChildren` property, we set a timing order for each link. Each link will take 0.5 seconds to appear one after the other. This creates a nice visual cue when the `Nav` is opened. In the `linkVariants` we animate the opacity and the vertical position of each link.

```jsx
<div className="App">
      <Header>
        <SvgBox
          variants={iconVariants}
          animate={isOpen ? "opened" : "closed"}
          onClick={() => setIsOpen(!isOpen)}
        >
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="https://www.w3.org/2000/svg"
          >
            <path
              d="M12 4C11.4477 4 11 4.44772 11 5V11H5C4.44772 11 4 11.4477 4 12C4 12.5523 4.44772 13 5 13H11V19C11 19.5523 11.4477 20 12 20C12.5523 20 13 19.5523 13 19V13H19C19.5523 13 20 12.5523 20 12C20 11.4477 19.5523 11 19 11H13V5C13 4.44772 12.5523 4 12 4Z"
              fill="#fff"
            />
          </svg>
        </SvgBox>
      </Header>
      <Nav
        initial={false}
        variants={menuVariants}
        animate={isOpen ? "opened" : "closed"}
      >
        <Link variants={linkVariants}>home</Link>
        <Link variants={linkVariants}>about</Link>
        <Link variants={linkVariants}>gallery</Link>
      </Nav>
</div>
```

Here, we pass in the variants to their respective components. In the `SvgBox`, we toggle the state of `isOpen` whenever it’s clicked, then conditionally animate it based on the state. Like the `SvgBox`, we conditionally animate the `Nav` and the `Link`s based on `isOpen`’s state.