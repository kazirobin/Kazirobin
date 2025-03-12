# Icon Shop

We can create interactive animations based on gestures. Motion components are currently able to listen for hover, tap, pan, and drag gesture detection. We’ll be building this [Icon Shop](https://codesandbox.io/s/icon-shop-0t3qg) app using the `whileHover` prop.

## All Components

- `App.js`: this holds the heading texts.
- `Card.jsx`: here, we define the animations for the icon cards.
- `CardContainer.jsx`: we import and loop through the icons.
- `styles.js`: create, style, and export the motion components. I used styled-components for styling the components.

Let’s start with `App.js`.

```jsx
import { H1, H2 } from "./Styles";
import CardContainer from "./CardContainer";

  return (
    <div>
      <H1 
        initial={{ y: -100 }} 
        animate={{ y: 0, transition: { delay: 1 } }}>
        Icon Shop
      </H1>
      <H2 
        initial={{ x: -1000 }} 
        animate={{ x: 0, transition: { delay: 1 } }}>
        Hover over the cards to see the motion magic
      </H2>
      <CardContainer />
    </div>
  );
```

We import the `H1` and `H2` motion components we created in the `Styles.js` file. Since they are motion components, we use the `initial` and `animate` props to define their behavior before and when they mount. Here, we also import and display the `CardContiner` component.

Now, the `CardContainer.js`.

```jsx
import { Container } from "./Styles";
import Card from "./Card";
import { ReactComponent as AddIcon } from "./assets/add.svg";
import { ReactComponent as AirplaneIcon } from "./assets/airplane.svg";
import { ReactComponent as AlarmIcon } from "./assets/alarm.svg";
//more svg imports below...

const icons = [
  <AddIcon />,
  <AirplaneIcon />,
  <AlarmIcon />,
  //more icons below
];

const CardContainer = () => {
  return (
    <Container initial={{ x: -1000 }} animate={{ x: 0 }}>
      {icons.map((icon) => (
        <Card icon={icon} />
      ))}
    </Container>
  );
};
```

Here, we import the SVGs, the `Container` motion component, and the `Card` component.

Similar to `H1` and `H2` in `App.js`, we define animations of the `Container` using the `initial` and `animate` props. When it loads, it will create a cool effect of sliding in from the left of the browser.

Now, `Card.js`

```jsx
import { CardBox, IconBox } from "./Styles";
const CardVariants = {
  beforeHover: {},
  onHover: {
    scale: 1.1
  }
};
const IconVariants = {
  beforeHover: {
    opacity: 0,
    y: -50
  },
  onHover: {
    opacity: 1,
    y: 0,
    scale: 1.5,
    transition: {
      type: "tween"
    }
  }
};

const Card = ({ icon }) => {
  console.log(icon);
  return (
    <CardBox variants={CardVariants} initial="beforeHover" whileHover="onHover">
      <IconBox variants={IconVariants}>{icon}</IconBox>
    </CardBox>
  );
};
```

Here, we create two variant objects with `beforeHover` and `onHover` animations. In the `CardVariants` object, we don’t want to do anything initially, so `beforeHover` is an empty object. `onHover` we increase the scale of the card box.

In the `IconVariants` object, we define the initial state of the `IconBox` in its `beforeHover`. We set its opacity to 0 and push it upwards by 50px. Then, in `onHover`, we set the opacity back to 1, push it back to its default position, and change the transition type to `tween`. Then we pass in the variants to their respective motion components. We make use of the propagation, so we don’t need to explicitly set the `initial` and `animate` props to the `IconBox` component.