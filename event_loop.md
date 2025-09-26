# Event Loop

The JavaScript event loop is a fundamental mechanism that enables asynchronous, non-blocking operations in a single-threaded environment. It continuously monitors the Call Stack and various queues, ensuring tasks are processed efficiently.

|   № | Content                                                                                                                  |
| --: | ------------------------------------------------------------------------------------------------------------------------ |
|   1 | [JavaScript is Single-Threaded](#javascript-is-single-threaded)                                                          |
|   2 | [What's Event Loop?](#whats-event-loop)                                                                                  |
|   3 | [What does it consist of Event Loop?](#what-does-it-consist-of-event-loop)                                               |
|   4 | [Types of Tasks in JavaScript](#types-of-tasks-in-javascript)                                                            |
|   5 | [How Event Loop works in JavaScipt?](#how-event-loop-works-in-javascipt)                                                 |
|   6 | [Crucial Points](#crucial-points)                                                                                        |
|   7 | [Examples:](#examples)                                                                                                   |
|   8 | [Example № 1 (Basic Synchronous and Asynchronous Code)](#example--1-basic-synchronous-and-asynchronous-code)             |
|   9 | [Example № 2 (Microtasks with Promises)](#example--2-microtasks-with-promises)                                           |
|  10 | [Example № 3 (Nested Microtasks)](#example--3-nested-microtasks)                                                         |
|  11 | [Example № 4 (Event Listener and Promises)](#example--4-event-listener-and-promises)                                     |
|  12 | [Example № 5 (Interleaving Promises and setTimeout)](#example--5-interleaving-promises-and-settimeout)                   |
|  13 | [Example № 6 (Nested Promises with setTimeout)](#example--6-nested-promises-with-settimeout)                             |
|  14 | [Example № 7 (Promise Chaining with setTimeout)](#example--7-promise-chaining-with-settimeout)                           |
|  15 | [Example № 8 (Mixing Promise Resolution with Delays)](#example--8-mixing-promise-resolution-with-delays)                 |
|  16 | [Example № 9 (Deeply Nested Promises in a Timer)](#example--9-deeply-nested-promises-in-a-timer)                         |
|  17 | [Example № 10 (Compining Chained Promises and Timer Nesting)](#example--10-compining-chained-promises-and-timer-nesting) |

**Useful links:**

- All examples I found here: [The JavaScript Event Loop Explained with Examples](https://medium.com/@ignatovich.dm/the-javascript-event-loop-explained-with-examples-d8f7ddf0861d)
- Very helpful video: [Event Loop от А до Я. Архитектура браузера и Node JS](https://www.youtube.com/watch?v=zDlg64fsQow&t=1292s)

## JavaScript is Single-Threaded

- JavaScript runs on a **single thread** (in the browser or Node.js).
- This means it can only do one thing at a time (it has one **call stack**).
- But apps need to handle things like user input, network requests, timers — **without blocking**.
- To solve this, JavaScript uses the event loop with the help of the Web APIs (in browsers) or libuv (in Node.js).

## What's Event Loop?

- **The Event Loop** is a JavaScript mechanism that manages the execution of asynchronous operations by continuously monitoring the call stack and the task queue.
- It allows JavaScript, which is single-threaded, to handle tasks like network requests, timers, and user interactions without blocking the main thread.
- The event loop picks tasks from the queue when the call stack is empty and adds them back to the call stack for execution, ensuring the application remains responsive and never blocked.

## What does it consist of Event Loop?

- **Call Stack** - Keeps track of function calls. When a function is invoked, it is pushed onto the stack. When the function finishes execution, it is popped off.
- **Web APIs** - Provides browser features like `setTimeout`, DOM events, and HTTP requests. These APIs handle asynchronous operations.
- **Task Queue** - Stores tasks waiting to be executed after the call stack is empty. These tasks are queued by `setTimeout`, `setInterval`, or other APIs.
- **Microtasks Queue** - A higher-priority queue for promises and MutationObserver callbacks. Microtasks are executed before tasks in the task queue.
- **Event Loop** - Continuously checks if the call stack is empty and pushes tasks from the microtask queue or task queue to the call stack for execution.

## Types of Tasks in JavaScript

- **Synchronous Tasks** - Executed immediately on the call stack `(e.g., function calls, variable declarations)`.
- **Microtasks** - High-priority asynchronous tasks, such as `Promise` callbacks, `queueMicrotask` and `mutatuibObserver`.
- **Macrotasks** - Lower-priority asynchronous tasks, like `setTimeout`, `setInterval`, and DOM events.

## How Event Loop works in JavaScipt?

![event-loop-img](/images/github_event_loop.png)

- **Call Stack:** This is where synchronous JavaScript code is executed. Functions are pushed onto the stack when called and popped off when they return. JavaScript is single-threaded, meaning only one operation can be processed at a time in the Call Stack.
- **Web APIs (or Node.js APIs):** When asynchronous operations like `setTimeout`, network requests `(e.g., fetch)`, or DOM events `(e.g., click)` are encountered, they are handed off to the browser's Web APIs (or Node.js APIs in a Node.js environment). These APIs handle the task in the background, allowing the Call Stack to continue processing other synchronous code.
- **Callback Queue (Task Queue/Macrotask Queue):** Once a Web API finishes its asynchronous task, it places the associated callback function into the Callback Queue. This queue holds tasks like `setTimeout` callbacks, `setInterval` callbacks, and I/O tasks (Input/Output task).
- **Microtask Queue:** This queue has a **higher priority** than the Callback Queue. It holds callbacks for promises (.then(), .catch(), .finally()) and MutationObserver callbacks.
- **Event Loop:** The Event Loop is the central orchestrator. It continuously performs the following checks:
  - Is the Call Stack empty? If the Call Stack is empty, it means all synchronous code has finished executing.
  - Is there anything in the Microtask Queue? If the Call Stack is empty, the Event Loop prioritizes processing all tasks in the Microtask Queue first, moving them to the Call Stack for execution one by one.
  - Is there anything in the Callback Queue? After the Microtask Queue is empty, the Event Loop then checks the Callback Queue and moves one task at a time to the Call Stack for execution.

This cycle repeats indefinitely, ensuring that asynchronous tasks are eventually executed without blocking the main thread, allowing for a responsive user interface and efficient handling of multiple operations.

## Crucial Points

- Microtasks (Promises) always execute before macrotasks `(setTimeout, setInterval, etc.)`
- Nesting Promises creates a queue of microtasks that execute in the same cycle.
- Timers (`setTimeout`) will always defer execution to the next event loop cycle, while microtasks resolve immediately after the current task.

## Examples

Let's check out knowledge in practice!

### Example № 1 (Basic Synchronous and Asynchronous Code)

```javascript
console.log("A"); // Synchronous

setTimeout(() => {
  console.log("B"); // Macrotask
}, 0);

console.log("C"); // Synchronous
```

**Output:** `A, C, B`

### Example № 2 (Microtasks with Promises)

```javascript
console.log("A"); // Synchronous

setTimeout(() => {
  console.log("B"); // Macrotask
}, 0);

Promise.resolve().then(() => {
  console.log("C"); // Microtask
});

console.log("D"); // Synchronous
```

**Output:** `A, D, C, B`

### Example № 3 (Nested Microtasks)

```javascript
Promise.resolve().then(() => {
  console.log("A");
  Promise.resolve().then(() => {
    console.log("B");
  });
});

console.log("C");
```

**Output:** `C, A, B`

### Example № 4 (Event Listener and Promises)

```javascript
document.body.addEventListener("click", () => {
  console.log("Click Event"); // Macrotask
});

Promise.resolve().then(() => console.log("Promise resolved"));

console.log("End");
```

**Output:** `End, Promise Resolved, Click Event`

### Example № 5 (Interleaving Promises and setTimeout)

```javascript
setTimeout(() => console.log("A"), 0);
Promise.resolve().then(() => console.log("B"));
setTimeout(() => console.log("C"), 0);
Promise.resolve().then(() => console.log("D"));
```

**Output:** `B, D, A, C`

### Example № 6 (Nested Promises with setTimeout)

```javascript
console.log("A"); // Synchronous

setTimeout(() => {
  // Macrotask
  console.log("B");
  Promise.resolve().then(() => console.log("C")); // Microtask
}, 0);

Promise.resolve().then(() => {
  // Microtask
  console.log("D");
  setTimeout(() => {
    // Macrotask
    console.log("E");
  }, 0);
});

console.log("F"); // Sunchronous
```

**Output:** `A, F, D, B, C, E`

### Example № 7 (Promise Chaining with setTimeout)

```javascript
console.log("1"); // Synchronous

setTimeout(() => {
  // Macrotasks
  console.log("2");
  Promise.resolve()
    .then(() => {
      console.log("3");
    })
    .then(() => {
      console.log("4");
    });
}, 0);

Promise.resolve() // Microtask
  .then(() => {
    console.log("5");
  })
  .then(() => {
    console.log("6");
  });

console.log("7"); // Synchronous
```

**Output:** `1, 7, 5, 6, 2, 3, 4`

### Example № 8 (Mixing Promise Resolution with Delays)

```javascript
console.log("Start"); // Synchronous

setTimeout(() => {
  // Macrotask
  console.log("Timeout #1");
}, 0);

Promise.resolve() // Microtask
  .then(() => {
    console.log("Promise #1");
    setTimeout(() => {
      // Macrotask
      console.log("Timeout #2");
    }, 0);
  })
  .then(() => {
    console.log("Promise #2");
  });

console.log("End"); // Synchronous
```

**Output:** `Start, End, Promise #1, Promise #2, Timeout #1, Timeout #2`

### Example № 9 (Deeply Nested Promises in a Timer)

```javascript
setTimeout(() => {
  // Macrotask
  console.log("Timeout #1");
  Promise.resolve().then(() => {
    // Microtask
    console.log("Promise #1");
    Promise.resolve().then(() => {
      // Microtask
      console.log("Promise #2");
    });
  });
}, 0);

Promise.resolve().then(() => {
  // Microtask
  console.log("Promise #3");
});

console.log("End"); // Synchronous
```

**Output:** `End, Promise #3, Timeout #1, Promise #1, Promise #2`

### Example № 10 (Compining Chained Promises and Timer Nesting)

```javascript
console.log("Start"); // Synchronous

setTimeout(() => {
  // Macrotask
  console.log("Timeout #1");
  Promise.resolve() // Microtask
    .then(() => {
      console.log("Promise #1");
    })
    .then(() => {
      console.log("Promise #2");
    });
}, 0);

Promise.resolve() // Microtask
  .then(() => {
    console.log("Promise #3");
    setTimeout(() => {
      // Macrotask
      console.log("Timeout #2");
    });
  })
  .then(() => {
    console.log("Promise #4");
  });

console.log("End"); // Synchronous
```

**Output:** `Start, End, Promise #3, Promise #4, Timeout #1, Promise #1, Promise #2, Timeout #2`
