# Stack & Queue

What is the difference between a Stack and a Queue? As a student studying Javascript that can be a little tricky to answer. Unlike other programming languages, Javascript does not have an explicit data structure for either a stack or a queue. So for a lot of self-taught programmers and Bootcamp grads they may not know how to use these more advanced data structures let how to build and implement them. The alternative is that they have been using them all along and never realized it. Get ready for a crash course is Stacks and Queues!

## Stack

Imagine that you have a stack of dinner plates to wash after you have dined with your family, and you are responsible to wash this stack of plates. How would you start it? Well, the obvious answer is: from the top.

A stack normally is a structure of sequential and ordered elements and it’s based on the principle of last in first out (LIFO). You can argue that sometimes you can remove an element from the middle of the stack without actually removing the plate from the top, and that’s a valid argument. But sometimes this solution might not work as expected. Imagine that in some situations we only have the option to remove the most recent element added to the stack.

![Screenshot_1.jpg](Stack%20&%20Queue%201b2aeacbb29981749903d201ea0db8d1/Screenshot_1.jpg)

A stack data structure follows the same principle and it’s called a LIFO data structure. LIFO means last in first out, the same way as a stack of dinner plates or other types of the stack in the real world works—the most recent element added to the stack should be the first out.

A stack data structure has two fundamental operations:

1. **push**—This operation is responsible for inserting or pushing a new element to the stack.
2. **pop**—This operation is responsible for removing the most recent element from the stack.

A stack is a linear data structure, which means that all elements are arranged in sequential order. It results that the push and pop operations can only happen at one end of the structure, in this case, the top of the stack.

Sometimes there can be more than two operations in a stack data structure. Sometimes we might use the isEmpty operation to check if the stack is empty, and the peek operation to return the top element without modifying the stack.

Now that we know about how the stack data structure works, let’s start the implementation in JavaScript.

The nice thing about working with stack data structures in JavaScript is that JavaScript already provides us the [**`push`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) and [**`pop`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) methods that we discussed. The `push` method adds an element to an array and the `pop` method removes the last element from an array.

We can start our stack by creating a new array named `stack`:

```jsx
let stack = [];
```

Now we can create our `push` operation. This function will be responsible for receiving an element as an argument and adding this element to our `stack`.

```jsx
const push = (item) => stack.push(item);
```

Now, we will create another operation called `pop`. This function will be responsible for removing the last element of the stack. Fundamentally it will be the last element added to the stack. Since we don’t know exactly which might be the last element of the stack, this function does not receive any argument.

```jsx
const pop = () => stack.pop();
```

We can also implement a stack data structure in JavaScript using classes. Here’s how we can do it:

```jsx
class Stack {
 constructor() {
   this.stack = [];
 }
 push(item) {
   this.stack.push(item);
 }
 pop() {
   this.stack.pop();
 }
}
```

Some developers like to implement stack data structures using linked lists instead of arrays in JavaScript. Although this might feel like a clever solution, the performance might not be the best one.

## Queue

Imagine that we have a line of people to enter a specific restaurant. The last person to get in the line will be the last person to enter the restaurant, depending on the size of the line. The first person that got into line will be the first person to enter the restaurant.

A queue is a linear structure of sequential and ordered elements, similar to a stack, with a difference that it works based on the principle of **first in first out (FIFO)**.

![Screenshot_2.jpg](Stack%20&%20Queue%201b2aeacbb29981749903d201ea0db8d1/Screenshot_2.jpg)

A queue data structure is called a FIFO data structure: It’s a structure of sequentially ordered elements in which the first element to be removed will be the first element added to the queue.

A queue data structure has two fundamental operations:

1. **enqueue**—This operation is responsible for inserting or pushing a new element to the queue.
2. **dequeue**—This operation is responsible for removing the oldest element from the queue.

Similar to a stack, we have a linear data structure, which means that all the operations in a queue can only happen at one end of the structure, in this case, the beginning of the queue.

JavaScript is a very helpful and handy language that provides us a lot of different methods to help us to achieve better results. The nice thing about JavaScript is that we also have a method to remove the first element of an array, which is the **`shift`** array method.

The implementation of a queue in JavaScript gets very simple and powerful. We can define our queue array like the following:

```jsx
let stack = [];
```

Now we can create our enqueue operation to add an element to our queue, exactly the same as we did with the stack example. Create a function called `enqueue` and pass an argument to this function, like this:

```jsx
const enqueue = (item) => queue.push(item);
```

Now we can create the function to remove the first element of our queue. We will create a function called `dequeue` and this function will be responsible for removing the first element of our queue.

```jsx
const dequeue = () => queue.shift();
```

Pretty easy, huh? But there are some hidden differences that we might not notice at first, specifically about performance.

Remember that both the `push` and `pop` methods have a time complexity of **O(1)**? The `shift` method has a time complexity of **O(n)**.

A simple difference in the time complexity of a piece of code can make a total difference in money, costs and performance for a company. If you’re planning to work with a queue data structure, the best possible idea is to create your own queue.

```jsx
function Queue() {
  this.queue = {};
  this.tail = 0;
  this.head = 0;
}

// Add an element to the end of the queue.
Queue.prototype.enqueue = function(element) {
  this.queue[this.tail++] = element;
}

// Delete the first element of the queue.
Queue.prototype.dequeue = function() {
  if (this.tail === this.head)
      return undefined

  var element = this.queue[this.head];
  delete element;
  return element;
}
```

Both stack and queue data structures are very flexible and easy to implement, but there are different use cases for each of them.

A stack is useful when we want to add elements inside a list into sequential order and remove the last element added. A queue is useful when we want the same behavior, but instead of removing the last added element, we want to remove the first element added to the list.