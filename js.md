# JS

## Types – knowledge of basic types and differences between them (primitives and non-primitive).

In JavaScript, types are categorized into two main groups: **primitive types** and **non-primitive types** (also known as reference types). Understanding these types is crucial for effective programming in JavaScript. Here’s an overview of both categories and the differences between them:

### Primitive Types

Primitive types are the basic building blocks in JavaScript. They are immutable, meaning their values cannot be changed once they are created. When you assign a primitive value to a variable, the variable directly holds the value.

#### Basic Primitive Types:

1. **Number**: Represents both integer and floating-point numbers.
   ```javascript
   let age = 25;          // integer
   let temperature = 23.5; // floating-point
   ```

2. **String**: Represents a sequence of characters enclosed in single quotes (`'`), double quotes (`"`), or backticks (`` ` ``) for template literals.
   ```javascript
   let name = "Alice";
   let greeting = `Hello, ${name}`;
   ```

3. **Boolean**: Represents a logical value, either `true` or `false`.
   ```javascript
   let isStudent = true;
   let hasGraduated = false;
   ```

4. **Undefined**: Represents a variable that has been declared but not yet assigned a value.
   ```javascript
   let myVar;
   console.log(myVar); // undefined
   ```

5. **Null**: Represents the intentional absence of any object value. It is used to signify that a variable is explicitly empty.
   ```javascript
   let emptyValue = null;
   ```

6. **Symbol**: Represents a unique and immutable value, often used as an object property key.
   ```javascript
   let uniqueSymbol = Symbol('description');
   ```

7. **BigInt**: Represents integers with arbitrary precision, useful for very large numbers.
   ```javascript
   let largeNumber = 1234567890123456789012345678901234567890n;
   ```

### Non-Primitive Types (Reference Types)

Non-primitive types, or reference types, are objects that can hold collections of values and more complex entities. They are mutable, meaning you can modify their contents. When you assign a non-primitive value to a variable, the variable holds a reference to the value, not the actual value itself.

#### Basic Non-Primitive Types:

1. **Object**: Represents a collection of key-value pairs. Objects can store various types of data, including other objects.
   ```javascript
   let person = {
     name: "Alice",
     age: 30,
     isStudent: false
   };
   ```

2. **Array**: Represents a list-like collection of values, which can be of any type. Arrays are a type of object with additional methods for handling collections.
   ```javascript
   let numbers = [1, 2, 3, 4, 5];
   let mixedArray = [1, "two", true, null];
   ```

  In JavaScript, arrays are indeed objects, which is why the `typeof` operator returns `'object'` for arrays. This can seem a bit surprising because arrays have special behaviors and methods that distinguish them from plain objects. Here's a bit of background on why this is the case:

  1. **JavaScript's Type System**: JavaScript has a very simple type system. At the core, it distinguishes between two main types: primitive values (like `number`, `string`, `boolean`, etc.) and objects. Arrays are a specialized type of object.

  2. **Internal Representation**: Under the hood, arrays in JavaScript are objects that come with additional properties and methods designed to handle ordered collections of data. They have a `length` property and other array-specific methods like `push`, `pop`, and `map`. But at their core, they use the same internal representation as objects.

  3. **`typeof` Operator**: The `typeof` operator in JavaScript is designed to return a string that indicates the type of the operand. For objects, including arrays, `typeof` returns `'object'`. This is why when you use `typeof` on an array, you get `'object'`.

  4. **Array.isArray()**: To distinguish arrays from other objects, JavaScript provides the `Array.isArray()` method. This method returns `true` if the value is an array and `false` otherwise. This helps in differentiating arrays from other object types, which `typeof` alone does not provide.

  So, while `typeof` tells you that arrays are objects, using `Array.isArray()` gives you a more specific way to check if a value is an array.

3. **Function**: Represents a block of code designed to perform a task. Functions in JavaScript are objects and can be assigned to variables, passed as arguments, and returned from other functions.
   ```javascript
   function greet(name) {
     return `Hello, ${name}`;
   }
   ```

4. **Date**: Represents date and time. It provides methods to handle and manipulate dates and times.
   ```javascript
   let now = new Date();
   ```

5. **RegExp**: Represents regular expressions, used for pattern matching within strings.
   ```javascript
   let pattern = /abc/;
   ```

### Differences Between Primitive and Non-Primitive Types

1. **Mutability**:
   - **Primitive Types**: Immutable. Once a primitive value is created, it cannot be changed.
   - **Non-Primitive Types**: Mutable. The contents of an object, array, or function can be changed after creation.

2. **Assignment**:
   - **Primitive Types**: When assigning a primitive value, a copy of the value is created.
     ```javascript
     let a = 10;
     let b = a; // b is a copy of a
     b = 20; // a remains 10
     ```
   - **Non-Primitive Types**: When assigning a non-primitive value, a reference to the value is created.
     ```javascript
     let obj1 = { name: "Alice" };
     let obj2 = obj1; // obj2 references the same object as obj1
     obj2.name = "Bob";
     console.log(obj1.name); // "Bob"
     ```

3. **Storage**:
   - **Primitive Types**: Stored directly in the stack (or a similar simple structure).
   - **Non-Primitive Types**: Stored in the heap, and variables hold references to these locations.

4. **Comparison**:
   - **Primitive Types**: Compared by value.
     ```javascript
     let x = 5;
     let y = 5;
     console.log(x === y); // true
     ```
   - **Non-Primitive Types**: Compared by reference.
     ```javascript
     let obj1 = { name: "Alice" };
     let obj2 = { name: "Alice" };
     console.log(obj1 === obj2); // false (different references)
     ```

5. **Default Values**:
   - **Primitive Types**: Can have default values like `undefined`, `null`, `0`, `""` (empty string), `false`, etc.
   - **Non-Primitive Types**: Default value is `null` if not initialized.

### Summary

- **Primitive Types** are the simplest data types, immutable, and compared by value.
- **Non-Primitive Types** (or reference types) are more complex, mutable, and compared by reference.

Understanding these differences helps in managing data and functions efficiently in JavaScript, optimizing performance, and avoiding common pitfalls in programming.


## Memory Management – knowledge of Garbage Collector concept, memory lifecycle, and data structures used to allocate memory (heap and stack).


Sure, let’s dive into JavaScript's memory management, including concepts related to garbage collection, memory lifecycle, and data structures like the heap and stack.

### Memory Management in JavaScript

Memory management in JavaScript is primarily handled by the JavaScript engine, which includes the garbage collector. The goal is to allocate and deallocate memory efficiently to ensure optimal performance of your application.

#### 1. **Heap and Stack**

- **Stack**:
  - The stack is used for static memory allocation. It stores primitive values (like numbers and booleans) and references to objects and functions. 
  - The stack follows Last In, First Out (LIFO) principle. When a function is called, a stack frame is created to store its local variables and other information. When the function returns, its stack frame is removed.

- **Heap**:
  - The heap is used for dynamic memory allocation. It’s where objects, arrays, and functions are allocated.
  - Unlike the stack, the heap does not follow LIFO. Memory is allocated and deallocated dynamically as needed, which can lead to fragmentation but allows for more flexible memory usage.

#### 2. **Garbage Collection**

- **Concept**:
  - Garbage collection (GC) is the process of automatically detecting and freeing up memory that is no longer in use, thus preventing memory leaks.
  - JavaScript engines, like V8 (used in Chrome and Node.js), use different algorithms for garbage collection. 

- **Types of Garbage Collection**:
  - **Reference Counting**: This method tracks the number of references to each object. When the reference count drops to zero, the object is considered unreachable and can be collected. This method can have issues with circular references.
  - **Tracing Garbage Collection**: This approach involves periodically identifying which objects are reachable from the root (e.g., global variables, local variables on the stack). The unreachable objects are then collected. Common methods include:
    - **Mark-and-Sweep**: Marks all reachable objects and sweeps away the unmarked ones.
    - **Mark-and-Compact**: Similar to mark-and-sweep, but it also compacts the heap to reduce fragmentation.

#### 3. **Memory Lifecycle**

- **Allocation**:
  - When a variable or object is created, memory is allocated from the heap or stack. For primitives, the memory is allocated on the stack. For objects and arrays, memory is allocated on the heap.

- **Usage**:
  - As your code runs, the memory is used for various operations and data. Proper usage patterns help manage memory efficiently. For example, large objects that are no longer needed should be dereferenced.

- **Deallocation**:
  - In JavaScript, you don’t manually deallocate memory. Instead, the garbage collector automatically frees up memory that is no longer reachable. For example, if you set a variable to `null` or let it go out of scope, the garbage collector may reclaim that memory if no other references to it exist.

#### 4. **Memory Leaks**

- **Common Causes**:
  - **Global Variables**: Unintentionally creating global variables can prevent garbage collection from working properly.
  - **Closures**: Closures that hold onto large objects or data can inadvertently prevent those objects from being collected.
  - **Detached DOM Nodes**: If DOM nodes are removed from the document but still referenced, they won’t be collected.
  - **Event Listeners**: Forgotten event listeners that keep references to large objects or DOM elements can lead to leaks.

- **Tools for Diagnosis**:
  - JavaScript engines and browsers provide tools to help diagnose memory issues. For example, Chrome’s DevTools have memory profiling and heap snapshot features to analyze memory usage and detect leaks.

### Summary

JavaScript’s memory management involves understanding how memory is allocated and deallocated, with the garbage collector handling the automatic cleanup of unused objects. The stack and heap are used for different types of data, and it’s important to be aware of common memory leak patterns to ensure your application remains performant and efficient.


## Closure – what is it and how it could affect application performance

A closure in JavaScript is a powerful concept that allows a function to retain access to its lexical scope even after it has finished executing. This can have significant implications for application performance and behavior. Let’s break it down:

### What is a Closure?

A closure occurs when a function is defined within another function, allowing the inner function to access variables from the outer function even after the outer function has returned. 

Here's a simple example:

```javascript
function outerFunction() {
  let outerVariable = 'I am from outerFunction';

  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

const myClosure = outerFunction();
myClosure(); // Logs: "I am from outerFunction"
```

In this example:
- `innerFunction` is a closure because it "closes over" the `outerVariable` defined in `outerFunction`.
- Even after `outerFunction` has returned, `innerFunction` still has access to `outerVariable`.

### How Closures Affect Application Performance

Closures can impact performance in various ways:

#### 1. **Memory Usage**

- **Retention of Scope**: Since closures retain references to their outer scope’s variables, this can lead to increased memory usage if not managed carefully. For example, if a closure captures a large object or a large number of variables, those references will persist as long as the closure exists.

- **Potential for Memory Leaks**: Closures that unintentionally hold onto large objects or resources can lead to memory leaks. For instance, if a closure is used as a callback or event handler and keeps references to large DOM elements, those elements won’t be garbage collected even if they are removed from the DOM.

#### 2. **Performance Overheads**

- **Increased Overhead**: Creating closures can introduce overhead in terms of memory and processing. Each closure maintains its own scope chain, which can add complexity to variable lookups. While this is usually minimal, it can add up in performance-critical sections of code or with many closures.

- **Long-lived Closures**: Closures that outlive their usefulness (for example, in long-lived global objects or as properties of objects) can lead to unnecessary memory consumption and potential performance degradation.

#### 3. **Impact on Garbage Collection**

- **Delayed Collection**: Because closures can hold references to variables, the garbage collector cannot reclaim memory used by these variables until the closure itself is no longer reachable. This can delay the cleanup of memory, especially if the closures are still in use or have been inadvertently retained.

### Best Practices to Manage Closures Effectively

1. **Be Mindful of Scope**: Understand the scope of variables that your closures are capturing. Avoid capturing large objects or unnecessary data.

2. **Avoid Unintended Retention**: Ensure that closures do not hold onto objects longer than necessary. For example, avoid using closures in global or long-lived contexts where they might retain large resources.

3. **Use Weak References**: In cases where you need to avoid preventing garbage collection, consider using weak references, such as `WeakMap` or `WeakSet`, which do not prevent their keys or values from being garbage collected.

4. **Clean Up Event Listeners**: When using closures in event listeners or callbacks, make sure to clean up these listeners when they are no longer needed to avoid memory leaks.

5. **Profile and Monitor**: Use profiling tools to monitor memory usage and identify potential issues with closures in your application.

### Summary

Closures are a fundamental concept in JavaScript that allows functions to retain access to their outer scope. While they offer powerful capabilities, they can impact application performance by increasing memory usage and potentially leading to memory leaks. By being mindful of how closures capture and retain data, and by following best practices for managing their lifecycle, you can mitigate performance issues and ensure efficient memory usage.


## `this` keyword - understand the full context and how it could be manipulated ( `call` , `apply` , `bind` )

The `this` keyword in JavaScript is a fundamental concept that refers to the context in which a function is executed. Understanding how `this` behaves in different scenarios is crucial for mastering JavaScript. Let’s explore the full context of `this`, how it can be manipulated using `call`, `apply`, and `bind`, and some common scenarios where `this` might behave unexpectedly.

### The `this` Keyword

In JavaScript, `this` refers to the object that is currently executing the code. Its value depends on the context in which a function is called:

1. **Global Context**:
   - In the global scope (outside of any function), `this` refers to the global object (`window` in browsers, `global` in Node.js).
   - Example:
     ```javascript
     console.log(this); // In a browser, this logs the window object
     ```

2. **Object Method**:
   - When a function is called as a method of an object, `this` refers to the object that the method is a property of.
   - Example:
     ```javascript
     const person = {
       name: 'Alice',
       greet: function() {
         console.log(this.name); // Logs 'Alice'
       }
     };
     person.greet();
     ```

3. **Constructor Function**:
   - When a function is invoked with the `new` keyword, `this` refers to the newly created instance of the constructor.
   - Example:
     ```javascript
     function Person(name) {
       this.name = name;
     }
     const alice = new Person('Alice');
     console.log(alice.name); // Logs 'Alice'
     ```

4. **Arrow Functions**:
   - Arrow functions do not have their own `this`. Instead, they inherit `this` from the surrounding lexical context (i.e., the `this` value of the enclosing function or scope).
   - Example:
     ```javascript
     const obj = {
       name: 'Alice',
       greet: function() {
         const inner = () => {
           console.log(this.name); // Inherits 'Alice' from obj
         };
         inner();
       }
     };
     obj.greet();
     ```

5. **Event Handlers**:
   - In event handlers, `this` refers to the element that triggered the event.
   - Example:
     ```javascript
     document.querySelector('button').addEventListener('click', function() {
       console.log(this); // Logs the button element
     });
     ```

### Manipulating `this` with `call`, `apply`, and `bind`

JavaScript provides methods to explicitly set or change the value of `this` in functions. These methods are `call`, `apply`, and `bind`.

1. **`call`**:
   - The `call` method invokes a function with a given `this` value and arguments provided individually.
   - Syntax:
     ```javascript
     function greet(greeting, punctuation) {
       console.log(`${greeting}, ${this.name}${punctuation}`);
     }
     const person = { name: 'Alice' };
     greet.call(person, 'Hello', '!'); // Logs: "Hello, Alice!"
     ```

2. **`apply`**:
   - The `apply` method is similar to `call`, but it takes arguments as an array.
   - Syntax:
     ```javascript
     function greet(greeting, punctuation) {
       console.log(`${greeting}, ${this.name}${punctuation}`);
     }
     const person = { name: 'Alice' };
     greet.apply(person, ['Hello', '!']); // Logs: "Hello, Alice!"
     ```

3. **`bind`**:
   - The `bind` method creates a new function with a specific `this` value and optional initial arguments. The returned function can be called later with or without additional arguments.
   - Syntax:
     ```javascript
     function greet(greeting, punctuation) {
       console.log(`${greeting}, ${this.name}${punctuation}`);
     }
     const person = { name: 'Alice' };
     const greetPerson = greet.bind(person, 'Hello');
     greetPerson('!'); // Logs: "Hello, Alice!"
     ```

### Common Pitfalls and Considerations

- **Lost Context**: Be cautious when passing methods around as callbacks or event handlers, as the context of `this` can be lost. Use `bind` to ensure the correct context if necessary.
- **Arrow Functions**: Remember that arrow functions do not have their own `this` context. They inherit it from their lexical scope.
- **Constructors and Methods**: Ensure that functions intended to be used as constructors are not inadvertently used as methods or standalone functions.

### Summary

The `this` keyword in JavaScript can be tricky to understand due to its dynamic nature. It depends on the context in which a function is called. By using `call`, `apply`, and `bind`, you can control and manipulate the value of `this`, allowing for more flexible and predictable function behavior. Understanding these concepts helps avoid common pitfalls and ensures that your code behaves as expected.


## Asynchronous Code – knowledge about callbacks and promises.
- How does JS handle asynchrony? (what mechanisms and language constructs does it offer to deal with it)?

- What are the sources of asynchrony in a web app?

Asynchronous programming is crucial in JavaScript, particularly for handling tasks like I/O operations, network requests, and UI updates without blocking the main execution thread. Let's explore how JavaScript handles asynchrony, focusing on callbacks, promises, and various mechanisms for managing asynchronous code.

### Understanding Asynchronous Code

#### Callbacks

- **What Are Callbacks?**
  - Callbacks are functions passed as arguments to other functions and executed after the completion of some operation. They are a fundamental way to handle asynchronous tasks in JavaScript.
  
- **Example of Callbacks:**
  ```javascript
  function fetchData(callback) {
    setTimeout(() => {
      const data = "Sample Data";
      callback(data);
    }, 1000);
  }
  
  fetchData((data) => {
    console.log(data); // Logs: "Sample Data"
  });
  ```

- **Pitfalls:**
  - **Callback Hell**: Nested callbacks can lead to deeply indented code that’s hard to read and maintain, known as "callback hell."
  - **Error Handling**: Handling errors can become cumbersome with callbacks.

#### Promises

- **What Are Promises?**
  - Promises represent a value that might be available now, later, or never. They provide a cleaner way to handle asynchronous operations compared to callbacks and can chain multiple asynchronous operations.

- **States of a Promise:**
  - **Pending**: The initial state, neither fulfilled nor rejected.
  - **Fulfilled**: The operation completed successfully.
  - **Rejected**: The operation failed.

- **Example of Promises:**
  ```javascript
  function fetchData() {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        const data = "Sample Data";
        resolve(data);
      }, 1000);
    });
  }
  
  fetchData()
    .then(data => {
      console.log(data); // Logs: "Sample Data"
    })
    .catch(error => {
      console.error(error);
    });
  ```

- **Chaining and Error Handling:**
  - Promises can be chained using `then` for handling successful results and `catch` for handling errors. The `finally` method can be used for cleanup regardless of success or failure.

### JavaScript's Asynchronous Mechanisms

JavaScript provides several constructs and mechanisms to handle asynchrony:

1. **Callbacks:**
   - Simple and direct, but can lead to complex and difficult-to-manage code when used extensively.

2. **Promises:**
   - Improve upon callbacks by providing a cleaner syntax for chaining operations and handling errors. They also allow for better error propagation.

3. **Async/Await:**
   - **Introduction:**
     - Introduced in ECMAScript 2017, `async` and `await` provide a more readable and synchronous-looking syntax for working with asynchronous code based on promises.
   - **Syntax:**
     ```javascript
     async function fetchData() {
       try {
         const response = await fetch('https://api.example.com/data');
         const data = await response.json();
         console.log(data);
       } catch (error) {
         console.error(error);
       }
     }
     
     fetchData();
     ```
   - **Key Points:**
     - `async` functions always return a promise.
     - `await` pauses execution within `async` functions until the promise resolves.

4. **Event Loop and Task Queue:**
   - **Event Loop:**
     - JavaScript runs in a single-threaded environment, but it uses the event loop to handle asynchronous tasks. The event loop continuously checks the call stack and task queue, executing tasks from the queue when the stack is empty.
   - **Task Queue (or Callback Queue):**
     - When asynchronous tasks (like I/O operations) complete, their callbacks are placed in the task queue. The event loop then processes these tasks when the call stack is clear.

5. **Web APIs and Microtasks:**
   - **Web APIs:**
     - Provided by the browser or runtime (like Node.js) to handle asynchronous operations (e.g., `setTimeout`, `fetch`, DOM events).
   - **Microtasks:**
     - Promises are managed in the microtask queue, which is processed before the next rendering phase.

### Sources of Asynchrony in a Web App

1. **Network Requests:**
   - Making HTTP requests using APIs like `fetch`, `XMLHttpRequest`, or libraries like Axios to retrieve data from servers.

2. **Timers:**
   - Using `setTimeout` or `setInterval` to schedule tasks to run after a delay or at regular intervals.

3. **User Interactions:**
   - Handling events like clicks, input changes, and other user interactions that trigger asynchronous handlers.

4. **Web Workers:**
   - Running scripts in background threads using Web Workers to perform heavy computations without blocking the main thread.

5. **File I/O:**
   - Reading or writing files, especially in Node.js environments, which can be done asynchronously to avoid blocking the event loop.

6. **DOM Manipulation:**
   - Certain DOM operations, especially those involving large changes or animations, can be asynchronous.

### Summary

JavaScript handles asynchrony through a variety of mechanisms, including callbacks, promises, and async/await. Understanding how `this` works in asynchronous contexts, along with the event loop, task queues, and various asynchronous sources, is essential for writing efficient and maintainable asynchronous code. Each mechanism has its own strengths and use cases, and modern JavaScript development often leverages promises and async/await for cleaner, more readable code.

## Event Loop - order of operations, micro, and macro task’s concept.

The event loop is a fundamental concept in JavaScript that manages the execution of asynchronous code and handles concurrency in a single-threaded environment. To understand how JavaScript handles asynchronous operations and manages tasks, it's essential to grasp the order of operations and the concepts of microtasks and macrotasks.

### Event Loop Overview

JavaScript is single-threaded, meaning it can execute one operation at a time. The event loop is responsible for managing and coordinating the execution of code, handling events, and processing asynchronous operations while ensuring that the execution remains smooth and non-blocking.

#### How the Event Loop Works

1. **Call Stack**:
   - The call stack is where JavaScript keeps track of function calls. Functions are pushed onto the stack when called and popped off when they complete. The stack operates on a Last In, First Out (LIFO) basis.

2. **Task Queue (or Callback Queue)**:
   - When asynchronous tasks (e.g., from `setTimeout`, `setInterval`, or I/O operations) are completed, their callbacks are placed into the task queue. The event loop will process these tasks when the call stack is empty.

3. **Microtask Queue (or Job Queue)**:
   - The microtask queue is a special queue for tasks that need to be executed as soon as possible after the currently executing script and before any other tasks. Microtasks are typically used for promise callbacks and `MutationObserver` callbacks.

4. **Rendering and Repainting**:
   - Browsers may perform rendering and repainting operations after processing all tasks in the queues to ensure smooth user experiences.

### Order of Operations

1. **Execute Synchronous Code**:
   - The event loop starts by executing all synchronous code in the call stack.

2. **Process Microtasks**:
   - After synchronous code execution, the event loop processes all tasks in the microtask queue. This ensures that promises and other microtasks are handled immediately after the synchronous code.

3. **Process Macrotasks**:
   - The event loop then processes tasks in the macrotask queue. Macrotasks include tasks from `setTimeout`, `setInterval`, and I/O operations.

4. **Rendering**:
   - After processing microtasks and macrotasks, the browser may perform rendering operations and repaint the screen.

5. **Repeat**:
   - The event loop continues to repeat this cycle, processing synchronous code, microtasks, macrotasks, and handling rendering as needed.

### Microtasks vs. Macrotasks

#### Microtasks

- **Definition**:
  - Microtasks are tasks that are scheduled to be executed immediately after the currently executing script and before any other tasks. They have higher priority over macrotasks.

- **Examples**:
  - **Promises**: The `then`, `catch`, and `finally` methods of promises are examples of microtasks.
  - **MutationObserver**: Observers that listen for changes in the DOM.

- **Execution**:
  - Microtasks are executed before any rendering or macrotasks. This ensures that promise resolutions and DOM mutations are handled promptly.

- **Example**:
  ```javascript
  console.log('Start');
  
  Promise.resolve().then(() => {
    console.log('Microtask 1');
  }).then(() => {
    console.log('Microtask 2');
  });
  
  console.log('End');
  ```
  - **Output**:
    ```
    Start
    End
    Microtask 1
    Microtask 2
    ```

#### Macrotasks

- **Definition**:
  - Macrotasks are tasks scheduled to be executed in the event loop cycle, typically from APIs such as `setTimeout`, `setInterval`, and I/O operations. They are also known as tasks or callback tasks.

- **Examples**:
  - **setTimeout**: Functions scheduled to run after a delay.
  - **setInterval**: Functions scheduled to run at regular intervals.
  - **I/O operations**: Reading files, network requests.

- **Execution**:
  - Macrotasks are processed after microtasks and can be deferred until the next cycle of the event loop.

- **Example**:
  ```javascript
  console.log('Start');
  
  setTimeout(() => {
    console.log('Macrotask 1');
  }, 0);
  
  setTimeout(() => {
    console.log('Macrotask 2');
  }, 0);
  
  console.log('End');
  ```
  - **Output**:
    ```
    Start
    End
    Macrotask 1
    Macrotask 2
    ```

### Example of Event Loop in Action

Consider the following example:

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Macrotask');
}, 0);

Promise.resolve().then(() => {
  console.log('Microtask');
});

console.log('End');
```

**Output:**
```
Start
End
Microtask
Macrotask
```

**Explanation:**
1. The synchronous code (`Start` and `End`) is executed first.
2. The microtask (`Promise.resolve().then(...)`) is processed immediately after the synchronous code.
3. The macrotask (`setTimeout(...)`) is processed after the microtasks are completed.

### Summary

The event loop is a key component of JavaScript’s concurrency model, allowing for non-blocking I/O operations in a single-threaded environment. It works by executing synchronous code, followed by microtasks, and then macrotasks, ensuring a responsive user experience. Understanding the distinction between microtasks and macrotasks helps in managing the execution flow and optimizing performance for asynchronous operations in JavaScript applications.


## Inheritance – knowledge about prototypes, object delegation, and the difference between a prototype and __proto__


Inheritance in JavaScript primarily relies on the prototype-based system rather than the classical inheritance models found in many other programming languages. Understanding prototypes, object delegation, and the difference between `prototype` and `__proto__` is crucial for mastering inheritance in JavaScript.

### Prototypes and Inheritance

#### Prototypes

- **What is a Prototype?**
  - In JavaScript, every object has an internal property called `[[Prototype]]` (often accessed via the `__proto__` property), which points to another object. This forms a prototype chain. When you attempt to access a property or method on an object, JavaScript first checks the object itself. If the property is not found, JavaScript looks up the prototype chain until it finds the property or reaches the end of the chain (`null`).

- **Prototype Chain**:
  - The prototype chain is a series of objects connected via their `[[Prototype]]` properties. This chain allows properties and methods to be inherited from parent objects.

- **Creating Prototypes**:
  - You can set up prototypes in various ways:
    - **Using Object Literals**:
      ```javascript
      const parent = {
        greet: function() {
          console.log('Hello from parent');
        }
      };
      
      const child = Object.create(parent);
      child.greet(); // Logs: 'Hello from parent'
      ```

    - **Using Constructor Functions**:
      ```javascript
      function Parent(name) {
        this.name = name;
      }
      
      Parent.prototype.greet = function() {
        console.log('Hello from parent');
      };
      
      function Child(name) {
        Parent.call(this, name); // Call parent constructor
      }
      
      Child.prototype = Object.create(Parent.prototype);
      Child.prototype.constructor = Child;
      
      const child = new Child('Alice');
      child.greet(); // Logs: 'Hello from parent'
      ```

    - **Using ES6 Classes**:
      ```javascript
      class Parent {
        greet() {
          console.log('Hello from parent');
        }
      }
      
      class Child extends Parent {
        constructor(name) {
          super(); // Calls the parent constructor
          this.name = name;
        }
      }
      
      const child = new Child('Alice');
      child.greet(); // Logs: 'Hello from parent'
      ```

#### Object Delegation

- **Object Delegation**:
  - JavaScript uses prototypes for delegation. When an object does not have a property or method, the JavaScript engine looks up the prototype chain. This delegation allows objects to share methods and properties without duplicating them.

- **Example of Delegation**:
  ```javascript
  const animal = {
    speak() {
      console.log('Animal speaks');
    }
  };
  
  const dog = Object.create(animal);
  dog.speak(); // Logs: 'Animal speaks'
  ```

  In this example, `dog` delegates the call to `speak()` to `animal` because `dog` does not have a `speak()` method of its own.

### `prototype` vs. `__proto__`

- **`prototype`**:
  - **Definition**: `prototype` is a property of constructor functions. It is used to define methods and properties that should be available to all instances created by that constructor.
  - **Usage**:
    ```javascript
    function Person(name) {
      this.name = name;
    }
    
    Person.prototype.sayHello = function() {
      console.log(`Hello, my name is ${this.name}`);
    };
    
    const john = new Person('John');
    john.sayHello(); // Logs: 'Hello, my name is John'
    ```
  - **Key Points**:
    - `prototype` is not a property of instances but a property of the constructor function.
    - The `prototype` object of a constructor function is shared by all instances created with that constructor.

- **`__proto__`**:
  - **Definition**: `__proto__` is an internal property (often accessed using `Object.getPrototypeOf()` and `Object.setPrototypeOf()` methods) that points to an object’s prototype. It is used for accessing or modifying the prototype chain of objects.
  - **Usage**:
    ```javascript
    const animal = {
      speak() {
        console.log('Animal speaks');
      }
    };
    
    const dog = {};
    dog.__proto__ = animal;
    dog.speak(); // Logs: 'Animal speaks'
    ```
  - **Key Points**:
    - `__proto__` is considered deprecated in favor of using `Object.getPrototypeOf()` and `Object.setPrototypeOf()`.
    - Changing `__proto__` directly is generally discouraged because it can lead to performance issues and code that is harder to understand and maintain.

### Summary

JavaScript uses a prototype-based inheritance model where objects inherit properties and methods from other objects via the prototype chain. The `prototype` property of constructor functions allows shared methods and properties for all instances, while `__proto__` is an internal property that points to an object’s prototype. Understanding these concepts and how they interact helps in leveraging JavaScript’s object-oriented capabilities effectively.


## What programming paradigms does Javascript support?

JavaScript is a versatile language that supports multiple programming paradigms, allowing developers to approach problems and design solutions in various ways. Here’s an overview of the key programming paradigms supported by JavaScript:

### 1. **Imperative Programming**

- **Definition**: Imperative programming is a paradigm where you instruct the computer on how to perform a task through a sequence of statements. It focuses on describing *how* to achieve a result.
- **Characteristics**:
  - **Control Flow**: Uses loops, conditionals, and control statements to dictate the execution flow.
  - **State Management**: Frequently involves managing the state of variables and objects.
- **Example**:
  ```javascript
  let total = 0;
  for (let i = 1; i <= 5; i++) {
    total += i;
  }
  console.log(total); // Logs: 15
  ```

### 2. **Declarative Programming**

- **Definition**: Declarative programming focuses on *what* the program should accomplish rather than *how* to achieve it. It abstracts away the control flow and focuses on describing the desired result.
- **Characteristics**:
  - **Expressiveness**: Often involves high-level constructs that describe operations and their outcomes.
  - **Abstraction**: The underlying implementation details are hidden from the developer.
- **Example**: 
  ```javascript
  const numbers = [1, 2, 3, 4, 5];
  const total = numbers.reduce((sum, num) => sum + num, 0);
  console.log(total); // Logs: 15
  ```

### 3. **Object-Oriented Programming (OOP)**

- **Definition**: Object-oriented programming is based on the concept of objects, which bundle data and behavior. It emphasizes encapsulation, inheritance, and polymorphism.
- **Characteristics**:
  - **Encapsulation**: Bundling data (properties) and methods (functions) into objects.
  - **Inheritance**: Creating new objects based on existing ones using prototypes or classes.
  - **Polymorphism**: Allowing objects to be treated as instances of their parent class or interface.
- **Example**:
  ```javascript
  class Animal {
    constructor(name) {
      this.name = name;
    }
    speak() {
      console.log(`${this.name} makes a noise.`);
    }
  }

  class Dog extends Animal {
    speak() {
      console.log(`${this.name} barks.`);
    }
  }

  const dog = new Dog('Rex');
  dog.speak(); // Logs: 'Rex barks.'
  ```

### 4. **Functional Programming**

- **Definition**: Functional programming treats computation as the evaluation of mathematical functions and avoids changing state and mutable data. It emphasizes immutability and functions as first-class citizens.
- **Characteristics**:
  - **Immutability**: Data is not modified after creation.
  - **Pure Functions**: Functions that return the same output given the same input and have no side effects.
  - **Higher-Order Functions**: Functions that can accept other functions as arguments or return functions.
- **Example**:
  ```javascript
  const add = (a, b) => a + b;
  const numbers = [1, 2, 3, 4, 5];
  const sum = numbers.reduce((acc, num) => add(acc, num), 0);
  console.log(sum); // Logs: 15
  ```

### 5. **Event-Driven Programming**

- **Definition**: Event-driven programming is based on the concept of events and handlers. Code execution is driven by events such as user interactions or messages from other programs.
- **Characteristics**:
  - **Event Handlers**: Functions that are triggered in response to events.
  - **Asynchronous Operations**: Handling events typically involves asynchronous operations.
- **Example**:
  ```javascript
  document.querySelector('button').addEventListener('click', () => {
    console.log('Button clicked!');
  });
  ```

### 6. **Asynchronous Programming**

- **Definition**: Asynchronous programming is a paradigm where tasks are performed independently of the main program flow, allowing for non-blocking execution.
- **Characteristics**:
  - **Callbacks**: Functions that are executed after an asynchronous operation completes.
  - **Promises**: Objects representing the eventual completion (or failure) of an asynchronous operation.
  - **Async/Await**: Syntax for working with promises in a more readable way.
- **Example**:
  ```javascript
  // Using Promises
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  
  // Using Async/Await
  async function fetchData() {
    try {
      const response = await fetch('https://api.example.com/data');
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error('Error:', error);
    }
  }
  
  fetchData();
  ```

### 7. **Prototype-Based Programming**

- **Definition**: Prototype-based programming is a form of object-oriented programming where objects inherit directly from other objects rather than from classes.
- **Characteristics**:
  - **Object Inheritance**: Objects can serve as prototypes for other objects.
  - **Dynamic Object Modification**: Objects can be modified at runtime, allowing for flexible inheritance and behavior modification.
- **Example**:
  ```javascript
  const parent = {
    greet() {
      console.log('Hello from parent');
    }
  };

  const child = Object.create(parent);
  child.greet(); // Logs: 'Hello from parent'
  ```

### Summary

JavaScript supports a range of programming paradigms, allowing developers to choose the most suitable approach for their problems. It includes:

- **Imperative** and **Declarative** programming for different approaches to expressing solutions.
- **Object-Oriented** programming for modeling real-world entities and their interactions.
- **Functional** programming for emphasizing pure functions and immutability.
- **Event-Driven** and **Asynchronous** programming for handling events and managing non-blocking operations.
- **Prototype-Based** programming for flexible and dynamic object-oriented designs.

Each paradigm provides different tools and methodologies for solving problems, making JavaScript a flexible and powerful language for various programming needs.


## How many threads does JS operate on? Can you do multithreading in JS? How?

JavaScript is primarily single-threaded, meaning it operates on a single execution thread for running code. However, it does offer mechanisms to handle concurrent and parallel operations, which can be thought of as forms of multitasking rather than true multithreading in the traditional sense. Here’s a detailed look at how JavaScript handles concurrency and whether it supports multithreading:

### Single-Threaded Nature

- **Single Thread**: JavaScript executes code in a single-threaded environment. This means it processes one piece of code at a time, in a sequential manner. This is managed through the event loop, which handles asynchronous operations without blocking the main thread.

### Concurrency and Asynchronous Operations

JavaScript achieves concurrency and handles asynchronous operations using:

1. **Event Loop**: Manages asynchronous tasks, allowing the program to perform non-blocking operations while waiting for events or I/O operations to complete.

2. **Callbacks, Promises, and Async/Await**: These mechanisms allow JavaScript to handle asynchronous code without blocking the execution thread. The event loop processes tasks from the callback queue and microtask queue, ensuring that asynchronous operations can be handled effectively.

### Web Workers (True Multithreading)

While JavaScript itself is single-threaded, you can achieve parallelism and multithreading through Web Workers. Web Workers provide a way to run scripts in the background on separate threads, which can be used to perform complex computations or handle tasks without blocking the main thread.

- **Web Workers**: Allow you to create multiple threads of execution that run concurrently. Each Web Worker runs in its own thread and has its own global context, separate from the main thread.
  
  - **Creation**: You create a worker by passing a URL to a script file that will be executed in the background.
    ```javascript
    // main.js
    const worker = new Worker('worker.js');
    
    worker.postMessage('Hello from main thread');
    
    worker.onmessage = function(event) {
      console.log('Message from worker:', event.data);
    };
    ```
    
    ```javascript
    // worker.js
    onmessage = function(event) {
      console.log('Message from main thread:', event.data);
      postMessage('Hello from worker thread');
    };
    ```

  - **Communication**: Workers communicate with the main thread using a messaging system. The `postMessage` method is used to send messages between the main thread and workers, and `onmessage` is used to receive messages.

  - **Limitations**:
    - Workers cannot access the DOM directly or modify it. They are designed for computational tasks or background processing.
    - Workers have their own global context (`self`), and you cannot share variables or functions directly between the main thread and workers.

### Other Multithreading and Parallelism Mechanisms

1. **SharedArrayBuffer and Atomics**:
   - **SharedArrayBuffer**: Allows shared memory between the main thread and workers, enabling low-level concurrency and parallelism.
   - **Atomics**: Provides atomic operations for managing shared memory safely and avoiding race conditions.
   - **Example**:
     ```javascript
     // main.js
     const buffer = new SharedArrayBuffer(1024);
     const view = new Int32Array(buffer);
     
     const worker = new Worker('worker.js');
     worker.postMessage(buffer);
     
     // worker.js
     onmessage = function(event) {
       const view = new Int32Array(event.data);
       view[0] = 42; // Modify shared memory
     };
     ```

2. **OffscreenCanvas**:
   - **OffscreenCanvas**: Allows canvas rendering in workers. This can be used for performing graphics and image processing tasks in the background.
   - **Example**:
     ```javascript
     // main.js
     const worker = new Worker('worker.js');
     const canvas = document.createElement('canvas');
     const offscreen = canvas.transferControlToOffscreen();
     
     worker.postMessage({ canvas: offscreen }, [offscreen]);
     ```

   ```javascript
   // worker.js
   onmessage = function(event) {
     const canvas = event.data.canvas;
     const context = canvas.getContext('2d');
     context.fillStyle = 'red';
     context.fillRect(0, 0, canvas.width, canvas.height);
   };
   ```

### Summary

- **Single-Threaded Execution**: JavaScript itself runs on a single thread for executing code. The event loop handles asynchronous tasks without blocking the main thread.

- **Web Workers**: JavaScript supports multithreading through Web Workers, which allows scripts to run concurrently in background threads. This is suitable for tasks that are CPU-intensive or require background processing.

- **SharedArrayBuffer and Atomics**: Provide mechanisms for low-level concurrency and parallelism with shared memory.

- **OffscreenCanvas**: Enables rendering tasks in workers, improving performance for graphics and image processing.

While JavaScript’s core execution model is single-threaded, these tools and mechanisms provide ways to achieve parallelism and handle concurrent tasks effectively.


## What is the event loop? How does it work?

The event loop is a fundamental part of JavaScript's concurrency model, enabling non-blocking asynchronous operations in a single-threaded environment. It manages the execution of code, handles events, and ensures smooth and responsive applications.

Here’s a detailed explanation of what the event loop is and how it works:

### What is the Event Loop?

The event loop is a mechanism that continuously checks and processes tasks in the JavaScript environment. It coordinates the execution of code, handles asynchronous operations, and ensures that JavaScript remains non-blocking, allowing for smooth user interactions and performance.

### Key Components

1. **Call Stack**:
   - The call stack is a data structure that keeps track of function calls. Functions are pushed onto the stack when they are called and popped off when they return.
   - JavaScript executes one function at a time, following the Last In, First Out (LIFO) principle.

2. **Task Queues**:
   - **Macrotask Queue**: Also known as the task queue or callback queue, it holds tasks like `setTimeout`, `setInterval`, and I/O operations.
   - **Microtask Queue**: Also known as the job queue or next tick queue, it holds tasks from promises and `MutationObserver`. Microtasks have higher priority and are processed before macrotasks.

3. **Event Loop**:
   - The event loop monitors the call stack and the task queues. It processes tasks in the following order:
     1. **Execute Synchronous Code**: JavaScript starts by executing any code in the call stack.
     2. **Process Microtasks**: Once the call stack is clear, the event loop processes all tasks in the microtask queue.
     3. **Process Macrotasks**: After microtasks are processed, the event loop then processes tasks in the macrotask queue.
     4. **Rendering**: After processing tasks, the browser may perform rendering operations if needed (e.g., layout, painting).

### How the Event Loop Works

1. **Initialization**:
   - JavaScript starts by executing synchronous code, which is placed in the call stack.

2. **Handling Asynchronous Operations**:
   - Asynchronous operations (like `setTimeout` or network requests) are handled by Web APIs provided by the browser or Node.js. Once these operations are completed, their callbacks are placed into the appropriate task queues (macrotask or microtask queue).

3. **Processing the Call Stack**:
   - The event loop continuously checks the call stack. If the call stack is empty, it proceeds to process tasks from the task queues.

4. **Processing Microtasks**:
   - Microtasks are processed before macrotasks. The event loop will exhaust the microtask queue before moving to the next macrotask.

5. **Processing Macrotasks**:
   - The event loop processes tasks in the macrotask queue in the order they were added.

6. **Rendering and Repainting**:
   - After processing the tasks, the browser may perform rendering operations (like layout changes or painting) to update the user interface.

7. **Repeat**:
   - The event loop repeats this cycle, ensuring continuous handling of asynchronous operations and maintaining a responsive application.

### Example of Event Loop in Action

Consider this code snippet:

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Macrotask');
}, 0);

Promise.resolve().then(() => {
  console.log('Microtask');
});

console.log('End');
```

**Execution Steps:**

1. **Execute Synchronous Code**:
   - `console.log('Start');` is executed and logged.
   - `console.log('End');` is executed and logged.

2. **Process Microtasks**:
   - The promise's `then` callback is placed in the microtask queue and executed immediately after the synchronous code.
   - `console.log('Microtask');` is logged.

3. **Process Macrotasks**:
   - The `setTimeout` callback is placed in the macrotask queue and executed after microtasks are completed.
   - `console.log('Macrotask');` is logged.

**Output**:
```
Start
End
Microtask
Macrotask
```

### Summary

- **Single-Threaded Execution**: JavaScript runs in a single-threaded environment, where only one piece of code executes at a time.
- **Event Loop**: Manages the execution of synchronous and asynchronous code, ensuring that the application remains responsive.
- **Task Queues**: Includes microtask and macrotask queues, which are processed in a specific order by the event loop.
- **Rendering**: The browser may perform rendering operations between task queue processing cycles.

The event loop is crucial for handling asynchronous tasks efficiently, allowing JavaScript to perform operations like I/O, network requests, and UI updates without blocking the main thread.


## What is a closure? What is a Higher Order Function?

### What is a Closure?

A closure in JavaScript is a feature where a function retains access to its lexical scope even after it has finished executing. This allows a function to remember and access variables from its outer (enclosing) function, even when the inner function is executed outside of its original context.

#### Key Characteristics of Closures:

1. **Lexical Scoping**:
   - Closures leverage lexical scoping, meaning a function's scope is determined by where it is defined, not where it is called.

2. **Encapsulation**:
   - Closures enable encapsulation of variables and functions, providing a way to create private data or methods.

3. **Persistent State**:
   - Closures can be used to maintain state across multiple function calls, as the enclosed variables are preserved between calls.

#### Example of a Closure:

```javascript
function createCounter() {
  let count = 0; // `count` is a private variable for the `counter` function
  return function() {
    count += 1;
    return count;
  };
}

const counter = createCounter();
console.log(counter()); // Logs: 1
console.log(counter()); // Logs: 2
console.log(counter()); // Logs: 3
```

In this example:
- `createCounter` is an outer function that defines a private variable `count`.
- It returns an inner function that increments and returns the `count`.
- Even though `createCounter` has finished executing, the returned inner function (the closure) retains access to `count`, demonstrating the persistent state of closures.

### What is a Higher-Order Function?

A higher-order function is a function that either:
1. **Takes one or more functions as arguments**, or
2. **Returns a function as its result**.

Higher-order functions allow for abstraction and code reuse by treating functions as first-class citizens. They enable powerful patterns like function composition, currying, and decorators.

#### Characteristics of Higher-Order Functions:

1. **Function as Argument**:
   - Higher-order functions can accept functions as parameters. This allows you to pass behavior into other functions, enabling dynamic functionality.

2. **Function as Return Value**:
   - Higher-order functions can return functions. This allows for creating functions with customized behavior or creating new functions based on some logic.

#### Examples of Higher-Order Functions:

1. **Function as Argument**:

   ```javascript
   function map(array, callback) {
     let result = [];
     for (let i = 0; i < array.length; i++) {
       result.push(callback(array[i]));
     }
     return result;
   }

   const numbers = [1, 2, 3];
   const doubled = map(numbers, function(x) {
     return x * 2;
   });
   console.log(doubled); // Logs: [2, 4, 6]
   ```

   In this example, `map` is a higher-order function because it takes a function (`callback`) as an argument.

2. **Function as Return Value**:

   ```javascript
   function multiplyBy(factor) {
     return function(number) {
       return number * factor;
     };
   }

   const double = multiplyBy(2);
   const triple = multiplyBy(3);

   console.log(double(5)); // Logs: 10
   console.log(triple(5)); // Logs: 15
   ```

   In this example, `multiplyBy` is a higher-order function because it returns a new function based on the provided `factor`.

### Summary

- **Closure**: A closure is a function that retains access to its lexical scope, allowing it to remember and access variables from its outer function even after the outer function has finished executing.
- **Higher-Order Function**: A higher-order function is a function that either takes other functions as arguments or returns a function as its result, enabling flexible and reusable patterns in programming.

These concepts are fundamental in JavaScript for managing scope, abstraction, and functional programming patterns.

## What is a class in Javascript?

In JavaScript, a class is a special kind of function introduced in ECMAScript 6 (ES6) that provides a syntactical sugar for creating and working with objects and their prototypes. Classes make it easier to define and work with objects in a way that is more similar to classical object-oriented programming languages, but they are still based on JavaScript's prototype-based inheritance.

### Key Features of JavaScript Classes

1. **Class Declaration**:
   - You define a class using the `class` keyword. It serves as a blueprint for creating objects and managing their behavior.

   ```javascript
   class Person {
     constructor(name, age) {
       this.name = name;
       this.age = age;
     }

     greet() {
       console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
     }
   }
   ```

2. **Constructor**:
   - The `constructor` method is a special method for initializing new objects created from the class. It is called automatically when a new instance is created.

   ```javascript
   const alice = new Person('Alice', 30);
   alice.greet(); // Logs: 'Hello, my name is Alice and I am 30 years old.'
   ```

3. **Methods**:
   - Methods defined inside a class are prototype methods, meaning they are shared across all instances of the class.

   ```javascript
   class Person {
     constructor(name, age) {
       this.name = name;
       this.age = age;
     }

     greet() {
       console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
     }

     celebrateBirthday() {
       this.age += 1;
       console.log(`Happy ${this.age}th birthday, ${this.name}!`);
     }
   }
   ```

4. **Inheritance**:
   - Classes can extend other classes using the `extends` keyword, allowing for inheritance. The `super` keyword is used to call methods from the parent class.

   ```javascript
   class Employee extends Person {
     constructor(name, age, jobTitle) {
       super(name, age); // Call the parent class constructor
       this.jobTitle = jobTitle;
     }

     describeJob() {
       console.log(`${this.name} is a ${this.jobTitle}.`);
     }
   }

   const bob = new Employee('Bob', 40, 'Software Engineer');
   bob.greet(); // Logs: 'Hello, my name is Bob and I am 40 years old.'
   bob.describeJob(); // Logs: 'Bob is a Software Engineer.'
   ```

5. **Getters and Setters**:
   - Classes can have getter and setter methods to define how properties are accessed and modified.

   ```javascript
   class Person {
     constructor(name, age) {
       this._name = name;
       this._age = age;
     }

     get name() {
       return this._name;
     }

     set name(newName) {
       this._name = newName;
     }

     get age() {
       return this._age;
     }

     set age(newAge) {
       if (newAge > 0) {
         this._age = newAge;
       }
     }
   }
   ```

6. **Static Methods**:
   - Static methods are defined on the class itself rather than on instances of the class. They are called on the class, not on instances.

   ```javascript
   class MathUtils {
     static add(x, y) {
       return x + y;
     }
   }

   console.log(MathUtils.add(5, 3)); // Logs: 8
   ```

### Under the Hood

Despite the class syntax providing a more familiar structure, JavaScript classes are essentially syntactic sugar over the existing prototype-based inheritance:

- **Class Definition**: Classes are converted into functions with prototype chains, and methods are added to the prototype.
- **Inheritance**: When a class extends another class, JavaScript sets up prototype chains to achieve inheritance.

### Summary

- **Class Declaration**: Use the `class` keyword to define a class, which provides a blueprint for creating objects.
- **Constructor**: Initializes new instances of the class.
- **Methods**: Define behavior shared among instances.
- **Inheritance**: Achieved using the `extends` keyword to create subclasses.
- **Getters and Setters**: Define how properties are accessed and modified.
- **Static Methods**: Defined on the class itself, not on instances.

JavaScript classes provide a clearer and more structured way to work with objects and inheritance compared to using functions and prototypes directly, while still retaining the flexibility of JavaScript's prototype-based system.


## What are the pros and cons of Promises?


Promises are a fundamental feature in JavaScript for managing asynchronous operations. They provide a way to handle asynchronous events more gracefully compared to traditional callback-based approaches. Here’s a detailed look at the pros and cons of using Promises:

### Pros of Promises

1. **Improved Readability and Maintainability**:
   - **Chaining**: Promises enable chaining of `.then()` methods, which can make asynchronous code more readable and easier to follow. This helps in avoiding deeply nested callbacks (callback hell).
   - **Error Handling**: Promises provide a centralized place for error handling with `.catch()` or `.finally()`, making it easier to manage errors across multiple asynchronous operations.

   ```javascript
   fetchData()
     .then(data => processData(data))
     .then(result => saveResult(result))
     .catch(error => handleError(error));
   ```

2. **Avoids Callback Hell**:
   - **Flat Structure**: Promises help in flattening the structure of asynchronous code, avoiding deeply nested callback functions and making the code more linear and easier to read.

   ```javascript
   // Callback Hell
   asyncOperation1(function(err, result1) {
     if (err) return handleError(err);
     asyncOperation2(result1, function(err, result2) {
       if (err) return handleError(err);
       asyncOperation3(result2, function(err, result3) {
         if (err) return handleError(err);
         // Continue processing
       });
     });
   });

   // Using Promises
   asyncOperation1()
     .then(result1 => asyncOperation2(result1))
     .then(result2 => asyncOperation3(result2))
     .catch(handleError);
   ```

3. **Consistency**:
   - **Uniform API**: Promises provide a consistent API (`.then()`, `.catch()`, `.finally()`) for handling asynchronous operations, making it easier to switch between different asynchronous sources or APIs.

4. **Better Error Handling**:
   - **Centralized Error Handling**: Promises make it straightforward to handle errors at any point in the chain. An error in any part of the chain can be caught with a single `.catch()` method at the end of the chain.

5. **Support for Asynchronous Operations**:
   - **Chaining and Composition**: Promises support chaining and composition, allowing multiple asynchronous operations to be combined and managed efficiently.

6. **Compatibility with Async/Await**:
   - **Integration with Async/Await**: Promises work seamlessly with `async`/`await` syntax, providing a more synchronous-looking code structure that improves readability and simplifies asynchronous code.

   ```javascript
   async function fetchData() {
     try {
       const response = await fetch(url);
       const data = await response.json();
       return data;
     } catch (error) {
       handleError(error);
     }
   }
   ```

### Cons of Promises

1. **Complexity**:
   - **Promise Chaining Complexity**: While chaining improves readability, it can still become complex with long chains of `.then()` calls, making it difficult to trace and debug.

2. **Error Handling**:
   - **Uncaught Errors**: If `.catch()` is not used, errors in promise chains can lead to unhandled promise rejections, which may not be caught or properly handled.

   ```javascript
   fetchData()
     .then(data => processData(data))
     .then(result => saveResult(result))
     // Missing .catch() here can lead to unhandled rejections
   ```

3. **No Built-in Cancellation**:
   - **Cancellation**: Promises do not natively support cancellation of asynchronous operations. Once a promise is created, it will resolve or reject regardless of whether you still need the result. This can be addressed with additional libraries or custom implementations.

4. **Verbosity**:
   - **Verbose Syntax**: For simple asynchronous operations, using promises can be more verbose than callbacks. In cases where only simple async operations are required, the additional syntax of promises might seem cumbersome.

5. **Error Propagation**:
   - **Error Propagation**: In complex chains, errors can propagate through multiple `.then()` blocks, and understanding the source of the error can be challenging if not properly managed.

### Summary

**Pros**:
- Improved readability and maintainability through chaining.
- Avoids callback hell with a flat structure.
- Consistent API for handling asynchronous operations.
- Centralized error handling with `.catch()`.
- Support for advanced patterns like chaining and composition.
- Seamless integration with `async`/`await` for cleaner syntax.

**Cons**:
- Complexity with long chains and nested promises.
- Potential for unhandled errors if `.catch()` is omitted.
- Lack of native cancellation support.
- Verbose syntax compared to simple callbacks.
- Error propagation can be challenging to debug in complex chains.

Promises are a powerful tool for managing asynchronous operations in JavaScript, but they require careful handling to avoid pitfalls. When used correctly, they provide a cleaner, more manageable way to work with asynchronous code compared to traditional callback-based approaches.


## what is async and await ?

`async` and `await` are JavaScript language features introduced in ECMAScript 2017 (ES8) that provide a more readable and concise way to work with asynchronous code. They are built on top of Promises and simplify the syntax for performing asynchronous operations. Here's a detailed overview of how `async` and `await` work and their benefits:

### What is `async`?

The `async` keyword is used to declare a function as asynchronous. An asynchronous function always returns a Promise, and it allows you to use the `await` keyword inside it.

#### Characteristics of `async` Functions:

1. **Returns a Promise**:
   - An `async` function automatically wraps its return value in a Promise. If the function returns a value, that value is automatically wrapped in a resolved Promise.

   ```javascript
   async function foo() {
     return 42;
   }
   
   foo().then(result => console.log(result)); // Logs: 42
   ```

2. **Use of `await`**:
   - Inside an `async` function, you can use the `await` keyword to pause the execution of the function until a Promise is resolved or rejected.

3. **Error Handling**:
   - Errors thrown inside an `async` function are returned as rejected Promises, allowing you to handle errors with `.catch()` or `try`/`catch` blocks.

### What is `await`?

The `await` keyword is used within an `async` function to pause its execution until a Promise is resolved or rejected. It allows you to write asynchronous code that looks and behaves like synchronous code.

#### Characteristics of `await`:

1. **Pauses Execution**:
   - When `await` is used, it pauses the execution of the `async` function until the Promise resolves. This makes it easier to read and write asynchronous code without deeply nested callbacks or `.then()` chains.

   ```javascript
   async function fetchData() {
     let response = await fetch('https://api.example.com/data');
     let data = await response.json();
     return data;
   }
   ```

2. **Error Handling**:
   - Errors in asynchronous operations can be caught using `try`/`catch` blocks.

   ```javascript
   async function fetchData() {
     try {
       let response = await fetch('https://api.example.com/data');
       let data = await response.json();
       return data;
     } catch (error) {
       console.error('Error fetching data:', error);
     }
   }
   ```

3. **Can Only Be Used in `async` Functions**:
   - The `await` keyword can only be used inside `async` functions. It will throw a syntax error if used outside of an `async` function.

### Example of `async` and `await` in Action

Here’s an example demonstrating how `async` and `await` work together:

```javascript

console.log("Start")
// Function to simulate fetching data from an API
function fetchDataFromAPI() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data from API');
    }, 2000);
  });
}

// Async function to handle the data fetching
async function getData() {
  try {
    console.log('Fetching data...');
    const data = await fetchDataFromAPI();
    console.log('Data received:', data);
  } catch (error) {
    console.error('Error:', error);
  }
}

// Calling the async function
getData();
console.log("End")
```

```console
Start
Fetching data...
End
Data received:Data from API
```


**Explanation**:
1. **`fetchDataFromAPI`**: Simulates an asynchronous operation returning a Promise that resolves after 2 seconds.
2. **`getData`**: Declared with `async`, it uses `await` to pause execution until `fetchDataFromAPI` resolves, making the asynchronous code look synchronous.
3. **Error Handling**: Errors in `fetchDataFromAPI` would be caught in the `catch` block.

### Benefits of `async`/`await`

1. **Readability**:
   - Provides a more synchronous-like syntax for asynchronous code, making it easier to read and understand.

2. **Error Handling**:
   - Simplifies error handling using `try`/`catch` blocks instead of chaining `.catch()` on Promises.

3. **Avoids Callback Hell**:
   - Reduces the complexity associated with nested callbacks, making the code more linear and easier to follow.

4. **Code Simplicity**:
   - Helps in avoiding the verbosity associated with chaining multiple `.then()` calls on Promises.

### Summary

- **`async`**: Declares a function that returns a Promise and allows the use of `await` within it.
- **`await`**: Pauses the execution of an `async` function until a Promise resolves, allowing for more readable and synchronous-like asynchronous code.

Using `async` and `await` makes handling asynchronous operations simpler and more intuitive, while still leveraging the underlying Promise-based mechanisms of JavaScript.

## API – knowledge about the difference between Cookies, Local Storage, and Session Storage.

Cookies, Local Storage, and Session Storage are three different mechanisms in web browsers used for storing data on the client side. Each has its own use cases, limitations, and characteristics. Here’s a detailed comparison:

### Cookies

**1. Definition**:
   - Cookies are small pieces of data stored by the browser and sent to the server with every HTTP request. They are used for various purposes, such as maintaining user sessions and storing user preferences.

**2. Size Limit**:
   - Each cookie can hold up to 4 KB of data, and browsers typically limit the number of cookies per domain (around 20-50).

**3. Expiration**:
   - Cookies have an expiration date and time, set using the `Expires` or `Max-Age` attribute. If not set, cookies expire when the session ends (i.e., when the browser is closed).

**4. Accessibility**:
   - Cookies are accessible both on the client-side (via `document.cookie`) and server-side (via HTTP headers).

**5. Security**:
   - **Transmission**: Cookies are sent with every HTTP request, which can expose them to security risks if not handled properly.
   - **Attributes**: Secure and HttpOnly flags can enhance security. `Secure` ensures cookies are sent only over HTTPS, and `HttpOnly` prevents client-side JavaScript from accessing the cookie.
   
**6. Use Cases**:
   - Session management (e.g., login sessions).
   - User preferences.
   - Tracking user behavior.

**7. Example**:
   ```javascript
   // Set a cookie
   document.cookie = "username=JohnDoe; expires=Fri, 31 Dec 2024 23:59:59 GMT; path=/";

   // Read a cookie
   const cookies = document.cookie;
   ```

### Local Storage

**1. Definition**:
   - Local Storage is part of the Web Storage API and allows storing data persistently in the browser without an expiration time. Data remains stored even after the browser is closed and reopened.

**2. Size Limit**:
   - Typically allows storage of up to 5-10 MB of data per origin.

**3. Expiration**:
   - Data in Local Storage persists indefinitely until explicitly deleted by the user or through JavaScript code.

**4. Accessibility**:
   - Local Storage is accessible only on the client-side via the `localStorage` object. It is not sent to the server with HTTP requests.

**5. Security**:
   - **Transmission**: Data in Local Storage is not sent with HTTP requests, reducing exposure to network-based attacks.
   - **Access**: Data is accessible to any script running on the same origin, which can be a security concern if XSS vulnerabilities exist.

**6. Use Cases**:
   - Storing user settings and preferences.
   - Caching data for offline use.
   - Maintaining non-sensitive user data.

**7. Example**:
   ```javascript
   // Set an item
   localStorage.setItem('username', 'JohnDoe');

   // Get an item
   const username = localStorage.getItem('username');
   ```

### Session Storage

**1. Definition**:
   - Session Storage is also part of the Web Storage API and allows storing data for the duration of a page session. Data is only available for the duration of the page session, which ends when the page is closed.

**2. Size Limit**:
   - Similar to Local Storage, it allows up to 5-10 MB of data per origin.

**3. Expiration**:
   - Data in Session Storage persists only as long as the browser tab or window is open. Once closed, the data is deleted.

**4. Accessibility**:
   - Session Storage is accessible only on the client-side via the `sessionStorage` object. It is not sent to the server with HTTP requests.

**5. Security**:
   - **Transmission**: Like Local Storage, data in Session Storage is not sent with HTTP requests, reducing exposure.
   - **Access**: Data is accessible to scripts running on the same origin and within the same session.

**6. Use Cases**:
   - Temporary storage of data needed during a single page session.
   - Data that should not persist beyond the current session or page view.

**7. Example**:
   ```javascript
   // Set an item
   sessionStorage.setItem('sessionData', 'temporaryValue');

   // Get an item
   const sessionData = sessionStorage.getItem('sessionData');
   ```

### Summary

**Cookies**:
- **Size Limit**: ~4 KB per cookie.
- **Expiration**: Can be set to expire or persist until manually deleted.
- **Accessibility**: Available on both client and server.
- **Use Case**: Session management, user tracking.

**Local Storage**:
- **Size Limit**: 5-10 MB per origin.
- **Expiration**: Persistent until explicitly deleted.
- **Accessibility**: Client-side only.
- **Use Case**: Persistent storage of non-sensitive data.

**Session Storage**:
- **Size Limit**: 5-10 MB per origin.
- **Expiration**: Data persists only for the duration of the page session.
- **Accessibility**: Client-side only.
- **Use Case**: Temporary storage for the duration of the page session.

Each storage mechanism serves different needs, and the choice among them depends on the nature of the data and its intended lifespan.

## Profiler and debugging – knowledge of how to debug performance issues.

Debugging performance issues and profiling are crucial tasks in optimizing web applications. Both tools and techniques help identify performance bottlenecks, memory leaks, and inefficient code. Here’s a detailed guide on how to debug performance issues and use profiling tools effectively:

### 1. **Understanding Performance Issues**

Performance issues can manifest in various ways, including:
- Slow page load times
- Laggy user interactions
- Memory leaks
- High CPU usage
- Long-running scripts

### 2. **Profiling Tools**

**1. Browser Developer Tools**

Modern browsers come with built-in developer tools that include powerful profiling and debugging features. Here’s how you can use them:

- **Google Chrome DevTools**: 

  - **Performance Tab**: 
    - Records and analyzes the performance of your application, including the event loop, rendering, and JavaScript execution.
    - Use it to identify long tasks, scripting bottlenecks, and layout/rendering issues.

    **Steps**:
    1. Open Chrome DevTools (F12 or right-click on the page and select “Inspect”).
    2. Go to the `Performance` tab.
    3. Click the record button, interact with your application, then stop the recording.
    4. Analyze the recorded data, including the timeline of events, CPU usage, and memory allocation.

  - **Memory Tab**:
    - Helps identify memory leaks and monitor memory usage.
    - Use it to take heap snapshots, analyze memory distribution, and track down detached DOM trees.

    **Steps**:
    1. Go to the `Memory` tab.
    2. Choose between `Heap snapshot`, `Allocation instrumentation on timeline`, or `Stack traces`.
    3. Take snapshots to analyze memory usage and identify leaks.

  - **Network Tab**:
    - Profiles network requests to analyze loading times and network performance.
    - Use it to identify slow network requests or large payloads.

    **Steps**:
    1. Go to the `Network` tab.
    2. Reload the page to capture network requests.
    3. Analyze request timings, sizes, and statuses.

- **Mozilla Firefox Developer Tools**:

  - **Performance Tool**:
    - Similar to Chrome’s Performance tab, it records and analyzes performance metrics.

    **Steps**:
    1. Open Firefox Developer Tools (F12).
    2. Go to the `Performance` tab.
    3. Record and analyze performance data.

  - **Memory Tool**:
    - Used to detect memory issues and analyze memory consumption.

    **Steps**:
    1. Go to the `Memory` tab.
    2. Take and analyze snapshots.

**2. **Third-Party Tools**

- **Lighthouse**:
  - An open-source tool integrated into Chrome DevTools that provides audits and performance insights.
  - Generates a report with performance scores, accessibility, best practices, and SEO.

  **Steps**:
  1. Open Chrome DevTools.
  2. Go to the `Lighthouse` tab.
  3. Generate a report for performance analysis.

- **WebPageTest**:
  - An online tool for performance testing from different locations and devices.
  - Provides detailed reports on load times, resource breakdowns, and suggestions for improvements.

  **Steps**:
  1. Go to [WebPageTest](https://www.webpagetest.org/).
  2. Enter your URL and run tests.
  3. Analyze the results and suggestions.

### 3. **Debugging Performance Issues**

**1. **Identify the Bottleneck**

- **Long Tasks**:
  - Look for tasks in the performance timeline that take longer than 50 ms. These can block the main thread and cause performance issues.

- **Rendering and Layout Issues**:
  - Identify excessive reflows and repaints by analyzing the layout and paint operations in the performance tab.

- **JavaScript Execution**:
  - Look for long-running scripts or functions that are blocking the main thread.

**2. **Optimize Code**

- **Minimize Layout Thrashing**:
  - Avoid frequent read and write operations that cause reflows and repaints.

- **Debounce and Throttle**:
  - Use debounce and throttle techniques to limit the frequency of function executions, especially for events like scrolling and resizing.

- **Code Splitting**:
  - Implement code splitting to load only the necessary code and reduce initial load times.

- **Avoid Memory Leaks**:
  - Ensure that event listeners, timers, and DOM elements are properly cleaned up to avoid memory leaks.

**3. **Use Efficient Data Structures**

- **Optimize Loops and Iterations**:
  - Use efficient algorithms and data structures to minimize time complexity and improve performance.

- **Leverage Web Workers**:
  - Use Web Workers to run scripts in background threads, freeing up the main thread for UI interactions.

**4. **Network Optimization**

- **Reduce Payload Size**:
  - Compress resources, use efficient formats, and minimize the size of network requests.

- **Leverage Caching**:
  - Use HTTP caching headers to reduce redundant network requests and improve load times.

### 4. **Best Practices**

- **Profile Regularly**:
  - Regularly profile your application during development to catch performance issues early.

- **Test on Real Devices**:
  - Test performance on various devices and network conditions to ensure a consistent user experience.

- **Monitor Production**:
  - Implement performance monitoring tools in production to track real-world performance metrics and issues.

### Summary

- **Profiler Tools**: Use browser developer tools (Chrome DevTools, Firefox Developer Tools) and third-party tools (Lighthouse, WebPageTest) to analyze performance and memory usage.
- **Debugging Techniques**: Identify performance bottlenecks, optimize code, use efficient data structures, and improve network performance.
- **Best Practices**: Regularly profile and test your application, monitor production performance, and implement optimization techniques.

By leveraging these tools and techniques, you can effectively debug performance issues and ensure a smoother, faster experience for your users.

## Browser Engine – how the browser reads HTML and applies the CSS styles.

Understanding how a browser engine reads HTML and applies CSS styles is crucial for optimizing web performance and ensuring that web pages render correctly across different devices. Here's a detailed overview of the process:

### 1. **Parsing HTML**

**1.1 **Loading HTML**:
   - When you request a web page, the browser fetches the HTML file from the server. The HTML content is then passed to the browser's rendering engine.

**1.2 **Tokenization**:
   - The HTML document is divided into tokens by the HTML parser. Tokens represent different parts of the HTML like tags, attributes, and text nodes.

**1.3 **Parsing HTML**:
   - The HTML parser constructs a Document Object Model (DOM) tree from the tokens. The DOM tree represents the structure and content of the HTML document.

   **Example**:
   ```html
   <html>
     <head>
       <title>Page Title</title>
     </head>
     <body>
       <h1>Hello World!</h1>
       <p>This is a paragraph.</p>
     </body>
   </html>
   ```
   The resulting DOM tree will have a structure with nodes corresponding to `<html>`, `<head>`, `<title>`, `<body>`, `<h1>`, and `<p>`.

### 2. **Parsing CSS**

**2.1 **Loading CSS**:
   - CSS stylesheets are fetched from the server if they are external, or they are extracted from `<style>` tags or inline styles in the HTML.

**2.2 **Tokenization**:
   - The CSS file is parsed into tokens representing CSS rules, selectors, and properties.

**2.3 **Parsing CSS**:
   - The CSS parser constructs a CSS Object Model (CSSOM) tree from the tokens. The CSSOM tree represents the styles associated with elements in the DOM.

   **Example**:
   ```css
   body {
     font-family: Arial, sans-serif;
   }

   h1 {
     color: blue;
   }

   p {
     color: green;
   }
   ```
   The resulting CSSOM will map styles to selectors like `body`, `h1`, and `p`.

### 3. **Combining DOM and CSSOM: Constructing the Render Tree**

**3.1 **Matching CSS to DOM**:
   - The browser combines the DOM tree and CSSOM to create a render tree. The render tree includes only the nodes that need to be rendered, along with their styles.

**3.2 **Render Tree Construction**:
   - For each element in the DOM, the browser calculates the styles based on the CSSOM. It constructs a render tree that includes visible elements and their computed styles.

   **Example**:
   - The `<h1>` element in the DOM is styled with a `color: blue` rule from the CSSOM. The render tree will include the `<h1>` node with the style applied.

### 4. **Layout and Painting**

**4.1 **Layout (Reflow)**:
   - The browser calculates the exact position and size of each element in the render tree based on the styles and the document’s layout. This process is known as reflow or layout.

   **Example**:
   - The browser calculates where to position the `<h1>` and `<p>` elements on the page and their size based on the font size and other CSS properties.

**4.2 **Painting**:
   - After layout, the browser paints the pixels to the screen. It draws each element according to the computed styles, such as colors, borders, and backgrounds.

   **Example**:
   - The `<h1>` element will be rendered with blue text, and the `<p>` element with green text, based on the painted styles.

### 5. **Rendering and Repainting**

**5.1 **Rendering**:
   - The final step is rendering the page, where the browser displays the content to the user.

**5.2 **Repainting**:
   - If changes are made to styles or the DOM after the initial rendering (e.g., through JavaScript), the browser may need to repaint certain parts of the page.

**5.3 **Reflow**:
   - Changes that affect layout (e.g., adding new elements, changing element sizes) may trigger a reflow, where the browser recalculates the layout.

### 6. **Optimization Techniques**

**6.1 **Minimize Reflows and Repaints**:
   - Minimize changes that require reflows or repaints to improve performance. Batch DOM changes and avoid layout thrashing.

**6.2 **Use Efficient CSS Selectors**:
   - Write efficient CSS selectors to minimize the time it takes to match styles with DOM elements.

**6.3 **Load CSS Early**:
   - Place CSS files in the `<head>` of the HTML document to ensure styles are applied before the page is rendered.

**6.4 **Defer Non-Critical CSS**:
   - Use techniques like media queries or loading CSS asynchronously for non-critical styles to improve initial page load times.

### Summary

1. **HTML Parsing**: The browser parses HTML to create a DOM tree representing the document’s structure.
2. **CSS Parsing**: The browser parses CSS to create a CSSOM tree representing the styles.
3. **Render Tree Construction**: The browser combines the DOM and CSSOM to build a render tree that includes visible elements and their styles.
4. **Layout and Painting**: The browser calculates element positions and sizes (layout) and then paints the pixels to the screen.
5. **Repainting and Reflow**: Changes to the DOM or styles may trigger repainting or reflow processes.

Understanding this process helps in optimizing web performance and ensuring that pages render efficiently and correctly across different browsers and devices.

## Polyfills – how to deal with browser differences.

Dealing with browser differences is a critical aspect of web development, especially when working with features that may not be uniformly supported across all browsers. Polyfills are one of the key strategies to address these discrepancies. Here’s a comprehensive guide on what polyfills are, how they work, and how to use them effectively.

### What are Polyfills?

**Definition**:
- A polyfill is a piece of code (usually JavaScript) that implements a feature on browsers that do not natively support it. Polyfills are used to ensure that your web application can use modern features even if the user’s browser doesn’t support them.

**Purpose**:
- To bridge gaps in browser compatibility by providing modern functionality in older or less capable browsers.

### How Polyfills Work

1. **Feature Detection**:
   - Polyfills often include a check to determine whether a feature is already supported by the browser. If the feature is missing, the polyfill implements it.

   **Example**:
   ```javascript
   if (!String.prototype.includes) {
     String.prototype.includes = function(search, start) {
       if (start === undefined) {
         start = 0;
       }
       return this.indexOf(search, start) !== -1;
     };
   }
   ```

   In this example, the `includes` method is added to `String.prototype` only if it doesn’t already exist.

2. **Implementation**:
   - If the feature is not supported, the polyfill provides a JavaScript implementation that mimics the functionality of the missing feature.

3. **Loading Polyfills**:
   - Polyfills can be included in your project as part of your build process, through external libraries, or conditionally loaded using scripts.

### Common Use Cases for Polyfills

1. **New JavaScript Features**:
   - For example, features like `Array.prototype.includes`, `Promise`, and `fetch` might need polyfills for older browsers.

2. **CSS Features**:
   - Polyfills can also be used for CSS features not supported by all browsers, like CSS Grid or custom properties.

3. **HTML Features**:
   - Features like HTML5 elements and APIs (e.g., `localStorage`, `Custom Elements`) may require polyfills in older browsers.

### Examples of Polyfills

**1. JavaScript Polyfill Example**:
   - Adding support for `Array.prototype.includes` in older browsers:

   ```javascript
   if (!Array.prototype.includes) {
     Array.prototype.includes = function(element) {
       return this.indexOf(element) !== -1;
     };
   }
   ```

**2. CSS Polyfill Example**:
   - Using PostCSS to add support for modern CSS features:

   ```bash
   npm install postcss postcss-preset-env
   ```

   ```javascript
   // postcss.config.js
   module.exports = {
     plugins: [
       require('postcss-preset-env')({
         stage: 0,
         features: {
           'custom-properties': true
         }
       })
     ]
   };
   ```

### Tools and Libraries for Polyfills

1. **Polyfill.io**:
   - A service that dynamically serves polyfills based on the user’s browser. You can include a script tag to automatically add the necessary polyfills.

   ```html
   <script src="https://polyfill.io/v3/polyfill.min.js"></script>
   ```

2. **Babel**:
   - Babel is a JavaScript compiler that can include polyfills for modern JavaScript features based on your target environments. Use the `@babel/polyfill` package or core-js.

   ```bash
   npm install @babel/polyfill
   ```

   ```javascript
   import '@babel/polyfill';
   ```

3. **Modernizr**:
   - A JavaScript library that detects HTML5 and CSS3 features in the user’s browser. You can use it to conditionally load polyfills based on feature support.

   ```html
   <script src="https://cdnjs.cloudflare.com/ajax/libs/modernizr/2.8.3/modernizr.min.js"></script>
   ```

4. **Core-JS**:
   - A modular standard library for JavaScript that includes polyfills for many ECMAScript features.

   ```bash
   npm install core-js
   ```

   ```javascript
   import 'core-js/stable';
   import 'regenerator-runtime/runtime';
   ```

### Best Practices for Using Polyfills

1. **Feature Detection**:
   - Always use feature detection rather than browser detection to apply polyfills. This ensures that polyfills are only loaded when needed.

2. **Minimize Polyfills**:
   - Load polyfills only for the features that are essential to your application. Avoid loading unnecessary polyfills to keep the page lightweight.

3. **Polyfill Loading**:
   - For performance optimization, load polyfills conditionally or only in specific environments. Tools like Polyfill.io can help with dynamic polyfilling.

4. **Testing**:
   - Test your application across different browsers and versions to ensure that polyfills work as expected and that the application performs well.

### Summary

**Polyfills**:
- **Definition**: Code that implements features on browsers that do not support them natively.
- **Purpose**: Ensures compatibility with modern features in older browsers.

**How They Work**:
- Detect feature support, implement missing functionality, and optionally load polyfills based on browser needs.

**Examples and Tools**:
- Use libraries like Polyfill.io, Babel, and Core-JS for JavaScript features.
- For CSS, use tools like PostCSS.

**Best Practices**:
- Feature detection, minimize polyfills, and test across browsers to ensure optimal performance and compatibility.

Using polyfills allows developers to leverage modern web features while maintaining compatibility with older browsers, thus providing a consistent experience for users across different environments.

## Explain Promise methods - .all(), .allSettled(), .race(), .any() and at the end summarize difference between them

Promises are a core feature of JavaScript that allow for asynchronous operations to be handled in a more manageable way. Several static methods are provided by the `Promise` object to handle multiple promises concurrently. Here’s a detailed explanation of the commonly used Promise methods: `.all()`, `.allSettled()`, `.race()`, and `.any()`, along with a summary of their differences.

### Promise Methods

#### 1. **`Promise.all(iterable)`**

**Purpose**:
- `Promise.all` takes an iterable of promises (usually an array) and returns a single promise that resolves when all of the promises in the iterable have resolved, or rejects if any of the promises reject.

**Behavior**:
- If all promises resolve, `Promise.all` resolves with an array of their results, in the same order as the promises were passed.
- If any promise rejects, `Promise.all` immediately rejects with the reason from the first promise that rejected.

**Example**:
```javascript
const p1 = Promise.resolve(3);
const p2 = 42;
const p3 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'foo'));

Promise.all([p1, p2, p3]).then((values) => {
  console.log(values); // [3, 42, 'foo']
}).catch((error) => {
  console.log(error);
});
```

#### 2. **`Promise.allSettled(iterable)`**

**Purpose**:
- `Promise.allSettled` takes an iterable of promises and returns a single promise that resolves after all of the given promises have either resolved or rejected, with an array of objects that describe the outcome of each promise.

**Behavior**:
- The result array contains objects with two properties for each promise: `status` (which will be either `"fulfilled"` or `"rejected"`) and `value` or `reason` (depending on the status).
- This method is useful when you need to know the result of all promises regardless of whether they are fulfilled or rejected.

**Example**:
```javascript
const p1 = Promise.resolve(3);
const p2 = Promise.reject(new Error('An error occurred'));
const p3 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'foo'));

Promise.allSettled([p1, p2, p3]).then((results) => {
  console.log(results);
  // [
  //   { status: 'fulfilled', value: 3 },
  //   { status: 'rejected', reason: Error: An error occurred },
  //   { status: 'fulfilled', value: 'foo' }
  // ]
});
```

#### 3. **`Promise.race(iterable)`**

**Purpose**:
- `Promise.race` takes an iterable of promises and returns a single promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects, with the value or reason from that promise.

**Behavior**:
- The returned promise will resolve or reject with the value or reason of the first promise that settles, regardless of the status of other promises.

**Example**:
```javascript
const p1 = new Promise((resolve, reject) => setTimeout(resolve, 500, 'first'));
const p2 = new Promise((resolve, reject) => setTimeout(resolve, 100, 'second'));

Promise.race([p1, p2]).then((value) => {
  console.log(value); // 'second'
});
```

#### 4. **`Promise.any(iterable)`**

**Purpose**:
- `Promise.any` takes an iterable of Promise objects and, unlike `Promise.all`, returns a single promise that resolves as soon as any of the promises in the iterable resolves. If no promises in the iterable resolve (i.e., all promises are rejected), it rejects with an `AggregateError`, a new subclass of `Error` that groups together multiple errors.

**Behavior**:
- Resolves with the first fulfilled promise's value. If all promises are rejected, it rejects with an `AggregateError`.

**Example**:
```javascript
const p1 = Promise.reject(new Error('Error 1'));
const p2 = Promise.reject(new Error('Error 2'));
const p3 = Promise.resolve('Success');

Promise.any([p1, p2, p3]).then((value) => {
  console.log(value); // 'Success'
}).catch((error) => {
  console.log(error); // AggregateError: All promises were rejected
});
```

### Summary of Differences

- **`Promise.all(iterable)`**:
  - **Resolves**: When all promises in the iterable have resolved.
  - **Rejects**: As soon as any of the promises reject.
  - **Result**: An array of results from the resolved promises.

- **`Promise.allSettled(iterable)`**:
  - **Resolves**: When all promises in the iterable have either resolved or rejected.
  - **Rejects**: Never, it always resolves.
  - **Result**: An array of objects indicating each promise’s outcome (`fulfilled` or `rejected`).

- **`Promise.race(iterable)`**:
  - **Resolves** or **Rejects**: As soon as one of the promises in the iterable resolves or rejects.
  - **Result**: The value or reason of the first promise that settles.

- **`Promise.any(iterable)`**:
  - **Resolves**: With the value of the first promise that fulfills.
  - **Rejects**: Only if all promises are rejected, with an `AggregateError`.
  - **Result**: The value of the first fulfilled promise, or an `AggregateError` if all promises fail.

These methods provide flexible ways to handle multiple asynchronous operations and manage their outcomes in various scenarios.

## Explain yield catchphrase in JavaScript

In JavaScript, `yield` is a keyword used in conjunction with generator functions to manage the control flow of code execution. It is part of the ECMAScript 2015 (ES6) specification and plays a key role in the creation of iterators, enabling functions to pause and resume their execution. Here’s a detailed explanation:

### **Generator Functions**

A generator function is defined using the `function*` syntax and allows you to define an iterative algorithm by writing a function that can yield multiple values over time. Unlike regular functions, which run to completion, generator functions can pause execution and return intermediate results using `yield`.

### **Yield Keyword**

- **Definition**: The `yield` keyword is used within a generator function to pause the function’s execution and return a value. When the generator function is called again, it resumes execution right after the `yield` statement.

- **Syntax**:
  ```javascript
  function* myGenerator() {
    yield 'first';
    yield 'second';
    yield 'third';
  }
  ```

### **How `yield` Works**

1. **Pausing Execution**: When the generator function encounters a `yield` statement, it pauses execution and returns the value following `yield`. The state of the generator function is saved, allowing it to be resumed later.

2. **Resuming Execution**: When the generator’s `next()` method is called again, the function resumes execution from where it was paused, immediately after the last `yield`.

3. **Iteration**: You can use the generator’s `next()` method to retrieve the next value yielded, and it returns an object with `value` and `done` properties. The `done` property indicates whether the generator has finished execution.

### **Example**

Here’s an example to demonstrate how `yield` works within a generator function:

```javascript
function* numberGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = numberGenerator();

console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }
```

### **Key Concepts with `yield`**

- **Iterator Protocol**: Generators adhere to the iterator protocol, meaning they have a `next()` method that returns `{ value, done }`. This protocol allows you to use generators in `for...of` loops and other iteration contexts.

- **Control Flow**: Generators provide a way to control the flow of code, especially useful in asynchronous programming, state management, and lazy evaluation.

- **Sending Values**: You can also send values into a generator function by using the `next()` method with an argument. The argument is passed to the generator function at the `yield` expression.

  ```javascript
  function* echoGenerator() {
    const input = yield 'Please provide input';
    yield `You provided: ${input}`;
  }

  const echo = echoGenerator();
  console.log(echo.next().value); // 'Please provide input'
  console.log(echo.next('Hello').value); // 'You provided: Hello'
  ```

### **Use Cases**

- **Lazy Evaluation**: Generators are ideal for lazy evaluation, where you only compute values when needed.
- **Asynchronous Programming**: They can be used to simplify asynchronous workflows, although modern JavaScript features like async/await have largely taken over this role.
- **Custom Iterators**: Generators provide a clean and manageable way to create custom iterators and control how values are generated.

### **Summary**

- **`yield`** is a keyword used inside generator functions to pause execution and return a value.
- **Generator functions** (`function*`) use `yield` to create iterable sequences of values and manage control flow.
- **Generators** support lazy evaluation and can simplify complex iteration and asynchronous programming patterns.

Using `yield` and generators allows you to create powerful, flexible iterators and manage execution flow in a more controlled manner.

## react strict mode during development

React's Strict Mode is a tool designed to help developers identify potential problems and improve the quality of their React applications during development. It provides additional checks and warnings for React components but does not affect the production build. Here’s an in-depth look at what React Strict Mode is, how it works, and why it’s useful:

### **What is React Strict Mode?**

React Strict Mode is a development-only tool introduced in React 16.3 that helps detect potential issues in your application by activating additional checks and warnings. It is not meant to be used in production and does not affect the runtime performance of the application.

### **How to Use Strict Mode**

To enable Strict Mode, you wrap your components or component tree with the `<React.StrictMode>` component. This can be done at the root level or within specific sections of your application.

**Example:**
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

### **Features and Benefits**

1. **Identifying Unsafe Lifecycles**
   - **What It Does**: React Strict Mode identifies components using unsafe lifecycle methods that may cause issues in future React versions. It warns about methods like `componentWillMount`, `componentWillReceiveProps`, and `componentWillUpdate`.
   - **Benefit**: Helps developers update components to use safer lifecycle methods, improving compatibility with future React updates.

2. **Detecting Unexpected Side Effects**
   - **What It Does**: Strict Mode invokes components twice (for class components) or in a more rigorous way (for functional components) to identify side effects that might not be properly cleaned up.
   - **Benefit**: Helps ensure that side effects and cleanups are handled correctly, reducing potential issues in production.

3. **Detecting Legacy Context API**
   - **What It Does**: Strict Mode warns if your application uses the old context API, which is considered legacy and may be removed in future versions.
   - **Benefit**: Encourages the use of the new context API, which is more robust and maintainable.

4. **Highlighting Potential Problems with Refs**
   - **What It Does**: React Strict Mode may provide warnings about using refs in ways that could cause problems, such as using them inappropriately or not cleaning them up.
   - **Benefit**: Ensures that refs are used correctly and that potential issues are addressed early.

5. **Detecting Multiple Render Issues**
   - **What It Does**: React Strict Mode helps identify if components have issues with rendering, such as unexpected multiple renders or inconsistent updates.
   - **Benefit**: Helps in debugging and improving the rendering performance and consistency of components.

6. **React Concurrent Features**
   - **What It Does**: Strict Mode helps test components in environments that simulate the behavior of concurrent rendering (a future feature of React).
   - **Benefit**: Prepares components for future concurrent rendering, improving compatibility with new features.

### **How It Works**

- **Double Invocation**: Strict Mode may intentionally double-invoke certain lifecycle methods and render phases in development to help identify side effects or issues. This is done to ensure that the component handles mounting and unmounting correctly.
  
- **Warnings and Errors**: Strict Mode activates additional warnings in the console for deprecated methods, potential issues with side effects, and other code that may cause problems in future versions of React.

### **Limitations**

- **Not for Production**: Strict Mode checks and warnings are development-only. It does not impact the production build, meaning it does not add overhead to your production code or affect runtime performance.
  
- **May Cause Noise**: In some cases, the additional warnings and checks may be noisy or intrusive, especially if the codebase has not yet been updated to use modern React practices.

### **Summary**

React Strict Mode is a powerful tool for improving the quality and maintainability of React applications during development. By identifying unsafe lifecycle methods, detecting side effects, and providing warnings about legacy features, it helps developers write more robust and future-proof code. While it adds no runtime overhead in production, its rigorous checks in development make it a valuable part of the React development workflow.


# TypeScript

## What is Typescript for? Advantages/disadvantages?

**TypeScript** is a statically typed superset of JavaScript developed by Microsoft. It introduces type annotations and other features to JavaScript to improve the development experience and code quality. TypeScript compiles down to plain JavaScript, which means it can run in any environment where JavaScript runs.

### What TypeScript Is For

**1. Type Safety:**
   - TypeScript allows developers to define types for variables, function parameters, return values, and object properties. This helps catch type-related errors at compile time rather than at runtime.

**2. Improved Development Experience:**
   - TypeScript provides enhanced tooling and editor support, including better autocompletion, type inference, and inline documentation. This can speed up development and reduce the likelihood of bugs.

**3. Enhanced Code Readability and Maintainability:**
   - Explicit types and interfaces make the code more readable and self-documenting, which aids in maintaining large codebases and collaborating with others.

**4. Object-Oriented Programming (OOP) Features:**
   - TypeScript supports OOP features such as classes, interfaces, and inheritance, which can help structure code more effectively and manage complexity.

**5. Better Refactoring:**
   - TypeScript's static type checking facilitates safer and more reliable refactoring. Tools can provide more accurate code suggestions and automatic refactoring options.

**6. Integration with JavaScript:**
   - TypeScript is designed to be a superset of JavaScript, meaning existing JavaScript code can be gradually adopted and converted to TypeScript. It allows for incremental adoption.

**7. Tooling and Ecosystem:**
   - TypeScript integrates well with build tools, IDEs, and editors. The TypeScript compiler (`tsc`) and type definition files (from `DefinitelyTyped` or `@types` packages) support a wide range of libraries and frameworks.

### Advantages of TypeScript

**1. Type Safety and Error Detection:**
   - **Advantage**: Early error detection during development helps prevent common runtime errors related to type mismatches.
   - **Example**: Catching issues like passing a string to a function that expects a number.

**2. Improved IDE Support:**
   - **Advantage**: Richer editor features such as autocompletion, type checking, and inline documentation enhance the development experience.
   - **Example**: IDEs like Visual Studio Code provide excellent TypeScript support with features like IntelliSense.

**3. Better Code Organization:**
   - **Advantage**: TypeScript's support for interfaces, classes, and modules helps in organizing and structuring code effectively.
   - **Example**: Using interfaces to define data shapes and classes for creating objects and managing state.

**4. Safer Refactoring:**
   - **Advantage**: TypeScript's static type checking makes code refactoring safer and more reliable, reducing the risk of introducing bugs.
   - **Example**: Renaming a method or property in a class automatically updates all references.

**5. Compatibility with JavaScript:**
   - **Advantage**: TypeScript is fully compatible with existing JavaScript code, allowing gradual adoption.
   - **Example**: You can start by renaming `.js` files to `.ts` and gradually add type annotations.

**6. Modern JavaScript Features:**
   - **Advantage**: TypeScript supports modern JavaScript features and provides additional features like decorators and generics.
   - **Example**: Using async/await, destructuring, and template literals.

**7. Rich Ecosystem:**
   - **Advantage**: TypeScript has a strong community and ecosystem, with many libraries providing type definitions.
   - **Example**: Libraries like `lodash` and `react` have comprehensive type definitions available.

### Disadvantages of TypeScript

**1. Learning Curve:**
   - **Disadvantage**: Developers need to learn TypeScript’s type system and additional syntax, which can be challenging for those unfamiliar with static typing.
   - **Example**: Learning how to use interfaces, generics, and type assertions.

**2. Compilation Step:**
   - **Disadvantage**: TypeScript requires a compilation step to convert `.ts` files into `.js` files. This adds complexity to the build process.
   - **Example**: Additional setup for build tools like Webpack or Babel to handle TypeScript.

**3. Increased Build Time:**
   - **Disadvantage**: The type-checking process can increase build times, especially in large projects.
   - **Example**: Large codebases with many type checks may take longer to compile.

**4. Type Definitions Maintenance:**
   - **Disadvantage**: Keeping type definitions up-to-date, especially for third-party libraries, can be a maintenance overhead.
   - **Example**: Updating type definitions when libraries release new versions.

**5. Potential for Overengineering:**
   - **Disadvantage**: Overusing complex type features can lead to overly complicated code, which might be harder to read and maintain.
   - **Example**: Excessive use of generics and advanced type constructs.

**6. Compatibility Issues:**
   - **Disadvantage**: Some older libraries or frameworks might not have TypeScript definitions or might not work well with TypeScript.
   - **Example**: Integrating TypeScript with older JavaScript libraries that lack type definitions.

### Summary of Differences

- **TypeScript vs. JavaScript**:
  - **Type Safety**: TypeScript offers static type checking, while JavaScript does not.
  - **Development Experience**: TypeScript provides better tooling support, including autocompletion and type inference.
  - **Build Process**: TypeScript requires a compilation step, whereas JavaScript runs directly in the browser or Node.js.
  - **Learning Curve**: TypeScript introduces additional concepts and syntax, whereas JavaScript is more straightforward.

In conclusion, TypeScript enhances JavaScript by adding static typing and other features that improve code quality, readability, and maintainability. However, it comes with its own set of challenges, including a learning curve and additional build steps. The choice between TypeScript and JavaScript often depends on the project requirements, team expertise, and the need for type safety and enhanced development tools.


## What’s the difference between an interface and a type?

In TypeScript, both `interface` and `type` are used to define types, but they serve slightly different purposes and come with their own sets of features and use cases. Here’s a detailed comparison of `interface` and `type`:

### **`interface`**

**1. **Definition**:
   - `interface` is used to define the shape of an object, including its properties and methods. It is specifically designed for defining contracts for classes or objects.

**2. **Extending**:
   - Interfaces can be extended using the `extends` keyword. Multiple interfaces can also be merged by declaring them with the same name.

**Example**:
   ```typescript
   interface Person {
     name: string;
     age: number;
   }

   interface Employee extends Person {
     employeeId: number;
   }

   const employee: Employee = {
     name: 'Alice',
     age: 30,
     employeeId: 12345,
   };
   ```

**3. **Declaration Merging**:
   - Interfaces support declaration merging, where multiple declarations with the same name are merged into a single interface.

**Example**:
   ```typescript
   interface Window {
     myProperty: string;
   }

   // Somewhere else in the code
   interface Window {
     myOtherProperty: number;
   }

   // Window now has both properties
   ```

**4. **Syntax**:
   - The syntax for defining interfaces is straightforward and designed to be expressive for object shapes.

**Example**:
   ```typescript
   interface Point {
     x: number;
     y: number;
   }
   ```

**5. **Use Cases**:
   - **Extending Classes**: Ideal for defining the shape of classes and their methods.
   - **Code Consistency**: Better for defining large object shapes with consistent properties.

### **`type`**

**1. **Definition**:
   - `type` can be used to define more complex types, including union types, intersection types, and mapped types. It’s a more flexible tool for defining a variety of types.

**2. **Extending**:
   - Types cannot be extended using `extends`. Instead, you can use intersection types (`&`) to combine multiple types.

**Example**:
   ```typescript
   type Person = {
     name: string;
     age: number;
   };

   type Employee = Person & {
     employeeId: number;
   };

   const employee: Employee = {
     name: 'Bob',
     age: 40,
     employeeId: 67890,
   };
   ```

**3. **Declaration Merging**:
   - Types do not support declaration merging. Each type must be uniquely named if you need different variations.

**4. **Syntax**:
   - The `type` keyword allows for defining more complex and composite types.

**Example**:
   ```typescript
   type Point = {
     x: number;
     y: number;
   };

   type Coordinates = Point | { lat: number; long: number };
   ```

**5. **Use Cases**:
   - **Union Types**: When you need a type that can be one of several types.
   - **Intersection Types**: When you need to combine multiple types into one.
   - **Complex Types**: For defining more intricate or composite types.

### **Comparison Summary**

- **Flexibility**:
  - **Interface**: Primarily used for defining object shapes and class contracts.
  - **Type**: More versatile, allowing complex types like unions, intersections, and mapped types.

- **Declaration Merging**:
  - **Interface**: Supports declaration merging (multiple declarations with the same name are merged).
  - **Type**: Does not support declaration merging (each `type` is unique).

- **Extending**:
  - **Interface**: Can be extended using `extends`, and multiple interfaces can be merged.
  - **Type**: Uses intersection types (`&`) to combine types, and does not support extension.

- **Use Cases**:
  - **Interface**: Best for defining shapes of objects, classes, and maintaining consistency across code.
  - **Type**: Best for creating complex types, unions, intersections, and when more flexibility is needed.

In general, you can use either `interface` or `type` based on the needs of your project. `interface` is well-suited for defining the structure of objects and class contracts, while `type` offers greater flexibility for defining complex or composite types. Many TypeScript developers prefer `interface` for object shapes and class definitions due to its extensibility and declaration merging capabilities, while `type` is often used for more complex type definitions and combinatorial scenarios.


## What do the following basic types mean: any , unknown , never , void

In TypeScript, the basic types `any`, `unknown`, `never`, and `void` have distinct purposes and characteristics. Understanding these types helps in writing more precise and robust TypeScript code. Here’s a detailed explanation of each:

### **`any`**

**Definition**:
- The `any` type represents any value and allows you to bypass TypeScript’s type checking. Variables of type `any` can hold any kind of value, and operations on them are allowed without type checking.

**Characteristics**:
- **Flexibility**: Offers no type safety. You can assign any value to a variable of type `any`.
- **Use Cases**: Useful when migrating JavaScript code to TypeScript or when dealing with values whose type is not known ahead of time.

**Example**:
```typescript
let data: any = 42;
data = "Hello";
data = { key: "value" };

// No type errors, since `any` bypasses type checking
const length: number = (data as string).length;
```

**Disadvantages**:
- **Lack of Type Safety**: Using `any` defeats the purpose of TypeScript’s static type checking and can lead to runtime errors.

### **`unknown`**

**Definition**:
- The `unknown` type is a safer alternative to `any`. It represents any value but requires you to perform some type checking before performing operations on it.

**Characteristics**:
- **Type Safety**: Provides type safety by requiring explicit type checks or type assertions before using the value.
- **Use Cases**: Useful when you want to handle values that could be of any type but still want to enforce type checking.

**Example**:
```typescript
let data: unknown = 42;
data = "Hello";

// TypeScript requires a type check or assertion before using `data`
if (typeof data === "string") {
  const length: number = data.length; // Safe because `data` is known to be a string
}
```

**Advantages**:
- **Enhanced Safety**: Ensures that you check the type before performing operations, thus preventing unexpected errors.

### **`never`**

**Definition**:
- The `never` type represents values that never occur. It is used to indicate that a function will never return a value or that a value should not be reachable.

**Characteristics**:
- **Unreachable Code**: Functions with a return type of `never` never complete normally and can be used for functions that throw exceptions or have infinite loops.
- **Type Checking**: It indicates code paths that should not be reached.

**Use Cases**:
- **Error Handling**: Functions that throw exceptions or terminate the program (e.g., `throw` statements).
- **Exhaustive Checks**: In `switch` statements or conditional branches to ensure all cases are handled.

**Example**:
```typescript
function throwError(message: string): never {
  throw new Error(message); // This function never returns
}

function infiniteLoop(): never {
  while (true) {
    // This function never completes
  }
}
```

**Advantages**:
- **Type Checking**: Helps TypeScript catch unreachable code or ensure all cases in a `switch` statement are handled.

### **`void`**

**Definition**:
- The `void` type represents the absence of a value. It is used primarily for functions that do not return a value.

**Characteristics**:
- **No Return Value**: Functions with a return type of `void` do not return a value.
- **Use Cases**: Commonly used for functions that perform side effects but do not produce a return value.

**Example**:
```typescript
function logMessage(message: string): void {
  console.log(message); // This function does not return anything
}
```

**Advantages**:
- **Clarity**: Makes it clear that a function is not expected to return a value.

### **Summary of Differences**

- **`any`**:
  - **Meaning**: Represents any value; no type checking.
  - **Use Cases**: When type is not known or when migrating from JavaScript.

- **`unknown`**:
  - **Meaning**: Represents any value but requires type checking before use.
  - **Use Cases**: When you need type safety while handling values of unknown type.

- **`never`**:
  - **Meaning**: Represents values that never occur; used for functions that don’t return normally.
  - **Use Cases**: Functions that throw errors or have infinite loops; exhaustive type checking.

- **`void`**:
  - **Meaning**: Represents the absence of a value; used for functions with no return value.
  - **Use Cases**: Functions that perform actions but do not return a value.

Each of these types plays a specific role in TypeScript, helping to define and enforce contracts, ensure type safety, and improve the robustness of the code.


# Exercises

## Implement a function that takes an array and returns a new array with the source array’s distinct elements:

https://jsfiddle.net/2yw6r47a/
```js
const EXAMPLE_ARRAY = [5, 1, 2, 6, 3, 2, 6, 5, 1, 2, 2];

function uniq(array){
  return array;
}

console.log(uniq(EXAMPLE_ARRAY));
```

For this fiddle and then share it with the candidate

Solution:
```js
const unique = (items: number[]) => [...new Set(items)];
```

### followup question:
Implement a function that takes an array and returns a new array with the source array’s distinct elements - WITHOUT Set

Assume that you want to maintain the order of elements and you cannot tell if Set holds the order of items passed.

Solution:
```ts
function unique(array: number[]) {
  const map = {};
  return array.reduce((acc, curr) => {
    if (map[curr]) {
      return acc;
    } else {
      map[curr] = true;
      return [...acc, curr]; //*
    }
  }, []);
}
```

### another follow-up question could be: what to change to have this array in reversed order?

Solution: `[curr, ...arr]`

## Implement a square animating from the left edge of the page 300px to the right. 

https://jsfiddle.net/ku6zsf4c/2/

```html
<div>
  <img src="https://i.imgur.com/runHReu.jpg" />
</div>
```

Solution:
```js
// scripts
const img = document.querySelector('img');

img.addEventListener('click', () => {
  img.classList.add('right')
});
```
```css
// styles
.right {
  transform: translateX(300px);
  transition: transform 1.0s;
}
```

## Implement your own Promise.all and Promise.race : 

https://jsfiddle.net/8m05zp3s/

Solution: 

```js
const promiseAll = (...promises) =>
  new Promise((resolve, reject) => {
    const results = [];
    promises
      .reduce(
        (acc, promise) =>
          acc
            .then(() => promise)
            .then((result) => results.push(result))
            .catch(reject),
        Promise.resolve(null)
      )
      .then(resolve);
  });

const promiseRace = (...promises) =>
  new Promise((resolve, reject) => {
    promises.reduce(
      (acc, promise) =>
        acc
          .then(() => promise)
          .then(resolve)
          .catch(reject),
      Promise.resolve(null)
    );
  });
```

## What will be printed out?

```js
Promise.resolve('PROMISE').then(x => console.log(x));
setTimeout(() => console.log('SET_TIMEOUT'), 0);
console.log('CONSOLE_LOG');
```

Solution:
```console
CONSOLE_LOG
PROMISE
SET_TIMEOUT
```

## What is debounce and throttle , implement one (or both) of them: 

https://jsfiddle.net/keLu0o4s/1

```html
<div>
  <button onclick="debouncedClickCb()">Debounced</button>
  <button onclick="throttledClickCb()">Throttled</button>
</div>
```
```js
const debounce = (fn, timeout) => fn;
const throttle = (fn, timeout) => fn;

const debouncedClickCb = debounce(() => console.log('DEBOUNCED CALLBACK'), 2000);

const throttledClickCb = throttle(() => console.log('THROTTLED CALLBACK'), 2000)
```

Solution:

```js
const debounce = function (fn, delay) {
  let timer;
  return function () {
    let context = this,
      args = arguments;
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(context, args);
    }, delay);
  };
};

function throttle(callback, wait) {
  let timeout = null;
  return (...args) => {
    if (!timeout) {
      callback(...args);
      timeout = setTimeout(() => (timeout = null), wait);
    }
  };
}

function throttle(fn, waitTimeMs) {
  let lastExecutionTime = 0;
  return function (...args) {
    let currentTime = Date.now();
    if (currentTime - lastExecutionTime >= waitTimeMs) {
      fn.apply(this, args);
      lastExecutionTime = currentTime;
    }
  };
}
```

## Write a function that will generate a random id

```js
const getPseudoRandomId = () => `${Date.now().toString(36)}-${Math.random().toString(36).substr(2)}`
```

### What is currying? Implement the curry function: 

https://jsfiddle.net/r79matoh/2/

```js
function sumOf3(x, y, z) { 
	return x + y + z 
};

function curry() {
	// TODO implement me
} 

console.log(curry(sumOf3)(1)(2)(3));
console.log(curry(sumOf3)(1)(2, 4));
console.log(curry(sumOf3)(1, 2)(5));
console.log(curry(sumOf3)(1, 2, 6));
```


Solution:

```js
// catch - the resulting function is "single use" because the cache is never cleared
function currySimple(fn) {
  let cache = [];
  return function curried(...args) {
    cache = [...cache, ...args];
    return cache.length >= fn.length ? fn(...cache) : curried;
  };
}
// the result is reusable and works correctly
const curryBetter =
  (fn) =>
  (...args) =>
    args.length >= fn.length
      ? fn(...args)
      : (...restArgs) => curryBetter(fn)(...args, ...restArgs);
```

## difference between commonjs and es6 module

CommonJS and ES6 (ECMAScript 2015) modules are two different module systems used in JavaScript to manage code dependencies and modularize code. Here's a comparison of the two:

### CommonJS Modules

**CommonJS** is a module system that originated in the Node.js ecosystem and is widely used for server-side JavaScript. Here are the key characteristics:

- **Syntax**: Uses `require` for importing and `module.exports` for exporting.
  ```javascript
  // Importing a module
  const moduleA = require('./moduleA');

  // Exporting from a module
  module.exports = {
    someFunction: function() {
      // ...
    }
  };
  ```

- **Loading**: Modules are loaded synchronously. This works well in server-side environments like Node.js but can be limiting for client-side code in browsers.

- **Scope**: Each module has its own scope. Variables and functions declared in one module are not visible to others unless explicitly exported.

- **Compatibility**: CommonJS modules are primarily used in Node.js. They are not natively supported in browsers, though tools like Browserify or Webpack can bundle CommonJS modules for browser use.

### ES6 Modules

**ES6 Modules** (also known as ES Modules) are part of the ECMAScript 2015 specification and are the standardized module system for JavaScript. Key characteristics include:

- **Syntax**: Uses `import` and `export` statements.
  ```javascript
  // Importing a module
  import { someFunction } from './moduleA';

  // Exporting from a module
  export function someFunction() {
    // ...
  }
  ```

- **Loading**: Modules are loaded asynchronously by default. This is useful for client-side JavaScript in browsers, allowing for more efficient code splitting and lazy loading.

- **Scope**: ES6 modules also have their own scope. Importing and exporting is more declarative and static, which allows for better optimizations by JavaScript engines.

- **Compatibility**: ES6 modules are natively supported in modern browsers and in recent versions of Node.js (with experimental support for older versions). They are the standard for both client-side and server-side JavaScript.

### Key Differences

1. **Loading Mechanism**:
   - **CommonJS**: Synchronous loading.
   - **ES6 Modules**: Asynchronous loading.

2. **Syntax**:
   - **CommonJS**: Uses `require()` and `module.exports`.
   - **ES6 Modules**: Uses `import` and `export`.

3. **Static vs. Dynamic**:
   - **CommonJS**: Modules are dynamic and can be altered after they are loaded.
   - **ES6 Modules**: Modules are static; imports and exports are resolved at compile time, allowing for better static analysis and tree-shaking.

4. **Default Exports**:
   - **CommonJS**: Uses `module.exports` for default exports.
   - **ES6 Modules**: Supports both named exports and default exports with `export default`.

5. **Module Resolution**:
   - **CommonJS**: Resolution is synchronous and occurs at runtime.
   - **ES6 Modules**: Resolution is asynchronous and occurs at compile time.

### Example of Both Module Systems

**CommonJS Example**:
```javascript
// math.js (CommonJS Module)
const add = (a, b) => a + b;
module.exports = { add };

// app.js
const math = require('./math');
console.log(math.add(2, 3)); // 5
```

**ES6 Module Example**:
```javascript
// math.js (ES6 Module)
export const add = (a, b) => a + b;

// app.js
import { add } from './math';
console.log(add(2, 3)); // 5
```

In summary, ES6 modules offer a standardized, more flexible module system with support for asynchronous loading and static analysis, whereas CommonJS remains a strong choice for server-side JavaScript with its synchronous loading and dynamic capabilities.