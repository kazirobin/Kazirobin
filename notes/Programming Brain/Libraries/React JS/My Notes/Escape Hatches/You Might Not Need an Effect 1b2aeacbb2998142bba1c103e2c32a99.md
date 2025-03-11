# You Might Not Need an Effect

Effects are an escape hatch from the React paradigm. They let you “step outside” of React and synchronize your components with some external system like a non-React widget, network, or the browser DOM. If there is no external system involved (for example, if you want to update a component’s state when some props or state change), you shouldn’t need an Effect. Removing unnecessary Effects will make your code easier to follow, faster to run, and less error-prone.

There are two common cases in which you don’t need Effects:

- **You don’t need Effects to transform data for rendering.** For example, let’s say you want to filter a list before displaying it. You might feel tempted to write an Effect that updates a state variable when the list changes. However, this is inefficient. When you update the state, React will first call your component functions to calculate what should be on the screen. Then React will “commit” these changes to the DOM, updating the screen. Then React will run your Effects. If your Effect *also* immediately updates the state, this restarts the whole process from scratch! To avoid the unnecessary render passes, transform all the data at the top level of your components. That code will automatically re-run whenever your props or state change.
- **You don’t need Effects to handle user events.** For example, let’s say you want to send an `/api/buy` POST request and show a notification when the user buys a product. In the Buy button click event handler, you know exactly what happened. By the time an Effect runs, you don’t know *what* the user did (for example, which button was clicked). This is why you’ll usually handle user events in the corresponding event handlers.

You *do* need Effects to synchronize with external systems. For example, you can write an Effect that keeps a jQuery widget synchronized with the React state. You can also fetch data with Effects: for example, you can synchronize the search results with the current search query. Keep in mind that modern frameworks provide more efficient built-in data fetching mechanisms than writing Effects directly in your components.

To help you gain the right intuition, let’s look at some common concrete examples!

[**Updating state based on props or state**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Updating%20state%20based%20on%20props%20or%20state%201b2aeacbb29981a08ad9da247a510801.md)

[**Caching expensive calculations**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Caching%20expensive%20calculations%201b2aeacbb299815cb104e40d50818c7b.md)

[**Resetting all state when a prop changes**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Resetting%20all%20state%20when%20a%20prop%20changes%201b2aeacbb29981e6a547e7bc1004186c.md)

[**Adjusting some state when a prop changes**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Adjusting%20some%20state%20when%20a%20prop%20changes%201b2aeacbb299819c9ec7ff16cba9c90b.md)

[**Sharing logic between event handlers**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Sharing%20logic%20between%20event%20handlers%201b2aeacbb299811eba78ef9d550fb994.md)

[**Sending a POST request**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Sending%20a%20POST%20request%201b2aeacbb2998124b070ca6b2a6193c8.md)

[**Chains of computations**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Chains%20of%20computations%201b2aeacbb29981359607cfad724b704a.md)

[**Initializing the application**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Initializing%20the%20application%201b2aeacbb299813fb9c5c4167861476a.md)

[**Notifying parent components about state changes**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Notifying%20parent%20components%20about%20state%20changes%201b2aeacbb299814ab986d9308aa595c1.md)

[**Passing data to the parent**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Passing%20data%20to%20the%20parent%201b2aeacbb29981cca363d211073da47b.md)

[**Subscribing to an external store**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Subscribing%20to%20an%20external%20store%201b2aeacbb299815fbc0ee89b3a8bf9c7.md)

[**Fetching data**](You%20Might%20Not%20Need%20an%20Effect%201b2aeacbb2998142bba1c103e2c32a99/Fetching%20data%201b2aeacbb29981c6974cdb3f5cc3c815.md)