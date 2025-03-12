# Animated Modal

We’ll build a modal component and learn about Framer Motion’s `AnimatePresence`, and how it allows us animate elements as they leave the DOM.

## All Components

- `App.js`: we set up the `showModal` state here.
- `Modal.jsx`: the actual animation work takes place here.
- `Styles.js`: create, style, and export the motion components. The components are styled using styled-components.

Let’s look into `App.js`

```jsx
import { ToggleButton, Container } from "./Styles";
import Modal from "./Modal";

function App() {
  const [showModal, setShowModal] = useState(false);
  const toggleModal = () => {
    setShowModal(!showModal);
  };
  return (
    <Container>
      <ToggleButton
        initial={{ x: -700 }}
        animate={{
          x: 0,
          transition: { duration: 0.5 }
        }}
        onClick={toggleModal}
      >
        Toggle Modal
      </ToggleButton>
      <Modal showModal={showModal} />
    </Container>
  );
}
```

We create a `showModal` state that will be used to conditionally render the modal. The `toggleModal` function will toggle the state whenever the `ToggleButton` is clicked. `ToggleButton` is a motion component, so we can define animations for it. When it mounts, it slides in from the left. This animation runs for 0.5 seconds. We also pass in the `showModal` state to the `Modal` through props.

Now, `Modal.jsx`

```jsx
import { AnimatePresence } from "framer-motion";
import { ModalBox, ModalContent, Container } from "./Styles";

<Container>
  <AnimatePresence>
    {showModal && (
      <ModalBox
        initial={{ opacity: 0, y: 60, scale: 0.3 }}
        animate={{
          opacity: 1,
          y: 0,
          scale: 1,
          transition: { type: "spring", stiffness: 300 }
        }}
        exit={{ opacity: 0, scale: 0.5, transition: { duration: 0.6 } }}
        >
        <ModalContent
          initial={{ y: -30, opacity: 0 }}
          animate={{ y: 0, opacity: 1, transition: { delay: 1 } }}
        >
           Modal content!!!!
        </ModalContent>
      </ModalBox>
    )}
  </AnimatePresence>
</Container>
```

We import `AnimatePresence` from `framer-motion`. It allows us to set exit animations for components when they leave DOM. We conditionally render the `Modal` based on the `showModal` state. We define the animations for the `ModalBox` and `ModalContent` through their `initial` and `animate` props. There’s also a new prop here, `exit`. Having `AnimatePresence` as a wrapper allows us to add exit animations to `ModalBox` in the `exit` prop.