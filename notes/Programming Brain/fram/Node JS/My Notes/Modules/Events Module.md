# Events Module

According to the official documentation of Node.js, it is an asynchronous event-driven JavaScript runtime. Node.js has an **event-driven architecture** which can perform asynchronous tasks. Node.js has **‘events’** module which emits named events that can cause corresponding functions or callbacks to be called. Functions(Callbacks) listen or subscribe to a particular event to occur and when that event triggers, all the callbacks subscribed to that event are fired one by one in order to which they were registered. **The EventEmmitter class:** All objects that emit events are instances of the EventEmitter class. The event can be emitted or listen to an event with the help of EventEmitter. 

## Syntax:

```jsx
const EventEmitter = require('events');
const eventEmitter = new EventEmitter();
```

**Listening events:** Before emits any event, it must register functions(callbacks) to listen to the events. 

```jsx
eventEmitter.addListener(event, listener)
eventEmitter.on(event, listener)
```

`eventEmmitter.on(event, listener)` and `eventEmitter.addListener(event, listener)` are pretty much similar. It adds the listener at the end of the listener’s array for the specified event. Multiple calls to the same event and listener will add the listener multiple times and correspondingly fire multiple times. Both functions return emitter, so calls can be chained. **eventEmitter.once(event, listener)** fires at most once for a particular event and will be removed from listeners array after it has listened once. Returns emitter, so calls can be chained. **Emitting events:** Every event is named event in nodejs. We can trigger an event by emit(event, [arg1], [arg2], […]) function. We can pass an arbitrary set of arguments to the listener functions. 

## Basic event handling methods

The Event emitter class works through callback mechanisms and contains two main methods that help us listen to and publish events:

- Event Subscription: `on`
- Event Publishing: `emit`

## Syntax:

```jsx
eventEmitter.emit(event, [arg1], [arg2], [...])
```

## Simple Event Example

```jsx
// Importing events
const EventEmitter = require('events');

// Initializing event emitter instances 
var eventEmitter = new EventEmitter();

// Registering to myEvent 
eventEmitter.on('myEvent', (msg) => {
console.log(msg);
});

// Triggering myEvent
eventEmitter.emit('myEvent', "First event");

// Output
// First event
```

## Extend the EventEmitter Class

It is recommended to make our own event emitter instance using class inheritance. As sometimes, in writing an app inheritance may affect scalability and performance. Class inheritance in Node.js is achieved using extending the base class.

```jsx
// Importing events
const EventEmitter = require("events");

// inheriting from EventEmitter class (parent class)
class MyEmitter extends EventEmitter {}

// Creating object of MyEmitter class (child class)
const myEmitter = new MyEmitter();

// Registering to myEvent
myEmitter.on("myEvent", (msg) => {
  console.log(msg);
});

// Triggering myEvent
myEmitter.emit("myEvent", "First event");

// Output
// First event
```

## Conclusion

- Events are Node.js modules that provide flexibility to the user to create, fire, and listen in the way the user desires.
- The Events module of Node.js provides us multiple functionalities that have got a variety of use cases when working on a real-time project like:
    - defining different event listeners for the same event
    - Passing an arbitrary number of arguments according to our need
    - handling errors etc.
- The on() method is used to create an event listener usually consisting of a callback function and the emit() method is used to trigger an event.
- All the callback functions are listened to by Node synchronously.