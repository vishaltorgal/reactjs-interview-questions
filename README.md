# React JS Interview Questions (2025–2026)

### Table of Contents

1. [State in React](#1-state-in-react)
2. [Difference Between State and Props](#2-difference-between-state-and-props)
3. [Higher Order Components (HOC)](#3-what-are-higher-order-components-hoc)
4. [Pure Components](#4-what-are-pure-components-in-react)
5. [Synthetic Events](#5-what-are-synthetic-events-in-react)
6. [Key Prop in Lists](#6-what-is-key-prop-and-what-is-the-benefit-of-using-it-in-arrays-of-elements)
7. [Virtual DOM](#6-what-is-virtual-dom)
8. [Controlled Components](#7-what-are-controlled-components)
9. [Uncontrolled Components](#8-what-are-uncontrolled-components)
10. [Fragments](#9-what-are-fragments)
11. [Stateful Components](#10-what-are-stateful-components)
12. [Function Components vs Class Components](#11-function-components-vs-class-components)
13. [Ways to Optimize React Application](#12-ways-to-optimize-react-application)
14. [useRef Hook](#13-useref)
15. [createRef](#14-createref)
16. [React Fiber](#15-what-is-react-fiber)
17. [Callback Function](#16-callback-function)
18. [Callback vs Higher Order Component (HOC)](#17-difference-callback-vs-higher-order-component-hoc)
19. [JavaScript Event Loop](#18-what-is-the-event-loop)
20. [Context API](#19-context-api)
21. [Custom Hooks](#20-custom-hook)

## 1. **State in React**

State is a built-in React object used to manage dynamic data within a component. It allows components to create and manage their own data, which can change over time based on user interactions or other factors.

### Key Points
- State is **mutable** and can be updated using `setState` in class components or the `useState` hook in functional components.
- When state is updated, React re-renders the component to reflect the new state.


### ***Class Component Example***
```jsx
import React from 'react';

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 }; // Initialize state
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 }); // Update state
  };

  render() {
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```

### ***Functional Component Example***
```jsx

import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Initialize state with useState

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button> {/* Update state */}
    </div>
  );
}

export default Counter;
```

<br>

## 2. **Difference Between State and Props**

### **State**
- State is a mutable data structure that holds information about the component itself.
- It can be updated using the `setState` method in class components or the `useState` hook in functional components.
- It is managed within the component and not accessible to other components unless explicitly passed.

### **Props**
- Props are read-only and are passed to the component by its parent.
- They are used to pass data and methods from parent to child components.
- They cannot be modified by the child component receiving them.

<br>

## 3. **What are Higher-Order Components (HOC)?**

A Higher-Order Component (HOC) is a pattern in React that allows you to reuse component logic. It is a function that takes a component and returns a new component with added functionality.

### Key Points
- HOC is a function: It takes a component and returns a new component.
- It doesn’t modify the original component: Instead, it enhances or adds features to it.
- Used for code reuse: HOCs allow for reusable functionality across multiple components (e.g., adding authentication checks, fetching data).

### ***Create the HOC***
```jsx

function withGreeting(Component) {
  return function WithGreeting(props) {
    return (
      <div>
        <h1>Hello, Welcome!</h1>
        <Component {...props} />
      </div>
    );
  };
}

export default withGreeting;
```

### ***Use the HOC with a component***

```jsx
import React from 'react';
import withGreeting from './withGreeting';  // Import the HOC

// Regular component that displays a message
function Message() {
  return <p>This is a message from the component.</p>;
}

// Wrap the Message component with the HOC
const MessageWithGreeting = withGreeting(Message);

function App() {
  return (
    <div>
      <MessageWithGreeting /> {/* HOC adds the greeting */}
    </div>
  );
}

export default App;
```
<br>

## 4. **What are Pure Components in React?**

A Pure Component in React is a type of component that only re-renders if its props or state have changed. In other words, it implements a shallow comparison of props and state, which helps improve performance by preventing unnecessary re-renders.

### Key Points
- It will always re-render whenever the parent re-renders, regardless of whether the props or state have changed.  
- React will perform a shallow comparison of props and state before re-rendering the component.
- If the props or state have not changed, React will skip the render, improving performance.

### ***Pure Component***

```jsx

import React, { PureComponent } from 'react';

class PureComponentExample extends PureComponent {
  render() {
    console.log('PureComponent re-rendered');
    return <h1>{this.props.name}</h1>;
  }
}

export default PureComponentExample;

```
<br>

## 5. **What are synthetic events in React?**

Synthetic Events are React's cross-browser wrapper around the browser's native events. They combine the behavior of different browsers into a single API to ensure consistent event handling.

### Key Points
- `Cross-Browser Compatibility`: Synthetic events normalize behavior across browsers.
- `Performance Optimization`: Synthetic events are pooled for efficiency, which means the same event object is reused for multiple events.
- `Consistent API`: React provides the same interface regardless of the browser.

```jsx
import React from 'react';

function SyntheticEventExample() {
  const handleClick = (event) => {
    console.log('Synthetic Event:', event); // React Synthetic Event
    console.log('Native Event:', event.nativeEvent); // Native DOM Event
  };

  return (
    <div>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default SyntheticEventExample;

```
<br>

## 6. **What is "key" prop and what is the benefit of using it in arrays of elements?**

A key is a special attribute you should include when mapping over arrays to render data. Key prop helps React identify which items have changed, are added, or are removed.

```jsx
const todoItems = todos.map((todo, index) => (
  <li key={index}>{todo.text}</li>
));
```
<br>

## 6. **What is Virtual DOM?**

The Virtual DOM (VDOM) is an in-memory representation of Real DOM. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called reconciliation.

### Key Points
- `Performance`: Updates to the real DOM are expensive. The Virtual DOM minimizes these updates by batching changes and updating the real DOM only when necessary.
- `Simplicity`: Developers can write declarative code without worrying about how to efficiently update the DOM.
- `Consistency`: The Virtual DOM helps ensure the UI is always in sync with the state.

### How the Virtual DOM Works
- `Initial Render` : When the component is first rendered, the Virtual DOM creates a virtual representation of the DOM elements.
- `Diffing Algorithm` : React uses a diffing algorithm to compare the new virtual DOM tree with the previous one.
- `Efficient Updates` : React updates only the parts of the real DOM that have changed, minimizing direct DOM manipulations.

<br>

## 7. **What are controlled components?**

Controlled components in React are form elements like `<input>`, `<textarea>`, and `<select>` where the value is controlled by React's state. The form element's value is set by the state, and any changes to the input are handled through event handlers that update the state.

```jsx
import React, { useState } from 'react';

function ControlledInput() {
  const [text, setText] = useState('');

  const handleChange = (e) => {
    setText(e.target.value);
  };

  return (
    <input type="text" value={text} onChange={handleChange} />
  );
}

export default ControlledInput;
```

### Key Points
- The value of the input is tied to the text state.
- The onChange handler updates the state when the user types, keeping the input value in sync with the state.

<br>

## 8. **What are Uncontrolled components?**

Uncontrolled components in React are form elements where the form data is handled by the DOM itself, rather than by React's state. In these components, you access the form values using refs, not state.

```jsx
import React, { useRef } from 'react';

function UncontrolledInput() {
  const inputRef = useRef(null);

  const handleSubmit = () => {
    alert(`Input value: ${inputRef.current.value}`);
  };

  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
}

export default UncontrolledInput;
```
### Key Points
- `Refs`: Use useRef to access the input's current value.
- `DOM Control`: The input value is managed by the DOM, not React state.
- `Use Case`: Useful when you need direct access to the DOM or for simple use cases where state management is not necessary.

<br>

## 9. **What are fragments?**

Fragments allow you to group multiple elements without adding extra nodes to the DOM. They help keep the DOM clean and avoid unnecessary wrapping elements like `<div>`.

```jsx
import React from 'react';

function FragmentExample() {
  return (
    <>
      <h1>Title</h1>
      <p>Description</p>
    </>
  );
}

export default FragmentExample;
```

### Key Points
- `Syntax`: Use empty tags <>...</> or <React.Fragment>...</React.Fragment>.
- `No Extra Nodes`: Fragments don’t add extra elements to the DOM.
- `Clean DOM`: Helps in keeping the DOM structure minimal and clean.
  

### list of reasons to prefer fragments over container DOM elements
- `Avoid Unnecessary DOM Nodes`: Fragments are a bit faster and use less memory by not creating an extra DOM node.
- `CSS Styling Simplicity`: When using fragments, you avoid having extra elements that require specific styles. With unnecessary wrapping elements, it might complicate applying styles or break layout constraints.
- `No Impact on Layout`: Unlike container elements like <div> or <span>, which could affect the layout (depending on their styles), fragments leave no trace in the layout rendering, thus maintaining the layout's intended structure.
  
<br>

## 10. **What are stateful components?**

A component is considered stateful if its behavior depends on its internal state. These stateful components can either be functional components with hooks or class components.

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);  // Declaring state

  const increment = () => {
    setCount(count + 1);  // Updating state
  };

  return (
    <div>
      <p>{count}</p>  {/* Displaying state */}
      <button onClick={increment}>Increment</button>
    </div>
  );
};
```

### Comparison with Stateless (Functional) Components
- `Stateful components` can modify and track their state over time.
- `Stateless components` (also called "dumb" components) do not manage their own state; they simply receive props from their parent component and render UI based on those props.

  <br>

## 11. **Function Components vs Class Components**

### When to Use Class Components:

- `Legacy Code`: If you're working with an existing codebase that already uses class components, it may be more efficient to continue using them to maintain consistency and avoid refactoring.
- `Familiarity`: If you're more familiar with class-based syntax or working with developers who prefer it, you might choose class components for a smoother transition.
- `Older React Features`: If you're working with older versions of React (pre-16.8) that don't support hooks, class components are required to manage state and lifecycle methods.

### When to Use Functional Components:

- `New Projects`: For new projects or codebases, prefer functional components as they align with modern React practices and offer cleaner, more maintainable code.
- `Hooks`: When you need state management, lifecycle methods, and side effects, use hooks in functional components, as they provide a more concise and flexible approach.
- `Performance`: Functional components with hooks tend to offer better optimization potential with React's latest features (like Concurrent Mode and Suspense).
- `Simplicity`: Functional components are typically more lightweight and easier to understand compared to class components, especially for small or medium-sized components.

### Summary
- Use class components when working with legacy code or when you have a specific reason based on your team's expertise.
- Use functional components for modern, efficient, and maintainable code, especially with hooks for state management and lifecycle features.

<br>

## 12. **Ways to optimize react application**

### Use PureComponent for Class Components
- `What it does`: Prevents re-renders if props and state are shallowly equal to the previous ones.
- `When to use`: For class components that don't require deep prop or state checks.

### Use useMemo Hook
- `What it does`: Memoizes expensive calculations to avoid recalculating on every render.
- `When to use`: For expensive computations inside functional components.

### Use useCallback Hook
- `What it does`: Memoizes callback functions to avoid re-creating them on every render.
- `When to use`: When passing functions down to child components.

### Lazy Loading and Code Splitting
- `What it does`: Breaks your app into smaller chunks and loads them only when needed, improving initial load time.
- `When to use`: For components that are not critical for the initial render.

### Debounce or Throttle Expensive Operations
- `What it does`: Limits the frequency of executing expensive operations like search or input handling.
- `When to use`: For search inputs, scroll events, etc.

### Optimize Image Loading
- `What it does`: Images are often the biggest assets in a React application. Using techniques like lazy loading, responsive images, and proper formats (e.g., WebP) can improve loading performance.
- `When to use`: Use loading="lazy" for images and consider srcset for responsive images.

<br>

## 13. **useRef**

`useRef` is a React hook that allows you to persist values across renders without causing a re-render.

### Key Points
- `Accessing DOM elements`: You can directly reference and interact with DOM elements (like focusing an input).
- `Storing mutable values`: You can store values (e.g., a counter or timer) that persist between renders but don’t trigger re-renders when changed.

```jsx
import React, { useRef } from 'react';

const Example = () => {
  const inputRef = useRef(); // Create a ref

  const focusInput = () => {
    inputRef.current.focus(); // Focus the input element
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus the input</button>
    </div>
  );
};
```
- useRef is used here to focus the input element when the button is clicked.
- It does not trigger re-renders when its value changes, which is useful for tasks like accessing DOM elements directly or tracking values without re-rendering the component.

<br>

## 14. **createRef**

`createRef` is a way to create a reference to a DOM element or a class component instance in React class components. It allows direct manipulation of the DOM or calling methods on class components without relying on state or props.

### Key Points
- `Used in class components`: createRef is specific to class components (not functional components).
- `Creates a reference`: It creates an object with a current property that refers to the DOM element or component instance.
- `Access DOM elements`: It helps you interact with DOM elements (like focusing an input or reading its value).
- `Access class component methods`: It allows interaction with methods in child class components.

```jsx
import React, { Component } from 'react';

class Example extends Component {
  constructor(props) {
    super(props);
    this.inputRef = React.createRef(); // Create a ref
  }

  focusInput = () => {
    this.inputRef.current.focus(); // Focus the input element
  };

  render() {
    return (
      <div>
        <input ref={this.inputRef} type="text" />
        <button onClick={this.focusInput}>Focus the input</button>
      </div>
    );
  }
}

export default Example;
```
<br>

## 15. **What is React Fiber?**

Fiber is the new reconciliation engine or reimplementation of core algorithm in React v16. The goal of React Fiber is to increase its suitability for areas like animation, layout, gestures, ability to pause, abort, or reuse work and assign priority to different types of updates; and new concurrency primitive

<br>

## 16. **Callback Function**

A `callback function` is a function passed as an argument to another function, to be called (invoked) later, usually after a task is completed.

### ***Class Component Example***
```jsx
function greetUser(name, callback) {
  console.log("Hello, " + name + "!");
  callback();
}

function sayGoodbye() {
  console.log("Goodbye!");
}

greetUser("Alice", sayGoodbye);

// Output
Hello, Alice!
Goodbye!

```
### In this example
- sayGoodbye is passed as a callback to greetUser.

- After greeting the user, it calls the callback() function.

<br>

## 17. **Difference Callback vs. Higher-Order Component (HOC)**

 ###  Definition:
A callback is a function passed as an argument to another function to be executed later, often after some operation is complete.

### Commonly Used For:
- Handling asynchronous behavior (e.g., API calls, event handling).

- Executing code after a function finishes.


### ***Callback Component Example***
```jsx
  function doSomething(callback) {
  console.log("Doing something...");
  callback();  // call the callback function
}

function afterDone() {
  console.log("Done!");
}

doSomething(afterDone);
```

 ###  Definition:
A Higher-Order Component is a function that takes a component and returns a new component. It's used to add additional behavior or logic to an existing React component.

### Commonly Used For:
- Code reuse in React apps.

- Adding cross-cutting concerns (e.g., authentication, logging, theming, etc.).


### ***Callback Component Example***
```jsx
  function withLogger(WrappedComponent) {
  return function EnhancedComponent(props) {
    console.log("Rendering:", WrappedComponent.name);
    return <WrappedComponent {...props} />;
  };
}

function Hello() {
  return <h1>Hello World</h1>;
}

const HelloWithLogger = withLogger(Hello);

```
<br>

## 18. **What is the Event Loop**

The JavaScript Event Loop is a mechanism that allows JavaScript (which is single-threaded) to perform non-blocking asynchronous operations, such as timers, network requests, and DOM events.

It continuously monitors the call stack and the message queues, executing tasks in the proper order — ensuring that asynchronous code runs only when the call stack is empty.

The Event Loop is what allows JavaScript to non-blockingly handle asynchronous events using:

- `Call Stack`: Where functions are executed.

- `Web APIs`: Where async tasks like setTimeout, fetch, etc., run.

- `Callback Queue (Task Queue)`: Where async callbacks wait to be executed.

- `Event Loop`: Keeps checking if the call stack is empty and then pushes the next task from the queue.


### ***Event Example***
```jsx
console.log("1. Start");

setTimeout(() => {
  console.log("2. Inside setTimeout");
}, 0);

Promise.resolve().then(() => {
  console.log("3. Inside Promise.then");
});
```

### ***Output***
```jsx
1. Start
4. End
3. Inside Promise.then
2. Inside setTimeout

```

- console.log("1. Start") and console.log("4. End") run immediately (synchronous).

- setTimeout(..., 0) is handled by the browser's Web API, and its callback is added to the task queue after at least 0ms.

- Promise.then() is added to the microtask queue, which runs before the task queue.

- So, Promise.then() logs before setTimeout.
  
- console.log("4. End");

<br>

## 19. **Context API **
The Context API is a built-in React feature used to create global state or shared values that can be accessed by any component in the tree, no matter how deep.
It solves "prop drilling" — the problem of passing props through multiple layers of components just to reach a deeply nested child.

### ***UserContext.js***
```jsx
import React, { createContext } from 'react';

export const UserContext = createContext();

export const UserProvider = ({ children }) => {
  const user = "Alice";

  return (
    <UserContext.Provider value={user}>
      {children}
    </UserContext.Provider>
  );
};

```

### ***DisplayUser.js***
```jsx
import React, { useContext } from 'react';
import { UserContext } from './UserContext';

const DisplayUser = () => {
  const user = useContext(UserContext);
  return <h2>Hello, {user}!</h2>;
};

export default DisplayUser;


```

### ***UWrap Your App with the Provider***
```jsx
// App.js
import React from 'react';
import { UserProvider } from './UserContext';
import DisplayUser from './DisplayUser';

const App = () => {
  return (
    <UserProvider>
      <DisplayUser />
    </UserProvider>
  );
};

export default App;

```

### ***Output***
```jsx
Hello, Alice!
```
<br>

## 20. **custom hook**

### ***useCounter.js**
```jsx
import { useState } from 'react';

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(c => c + 1);
  const decrement = () => setCount(c => c - 1);
  const reset = () => setCount(initialValue);

  return { count, increment, decrement, reset };
}

export default useCounter;

```

### ***Use the Hook in a Component***
```jsx
// CounterComponent.js
import React from 'react';
import useCounter from './useCounter';

function CounterComponent() {
  const { count, increment, decrement, reset } = useCounter(0);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={increment}>➕</button>
      <button onClick={decrement}>➖</button>
      <button onClick={reset}>🔁</button>
    </div>
  );
}

export default CounterComponent;

```

### Key Points
- Must start with use
- Only call hooks at the top level
- Only call hooks from:
    1. React function components, or
    2. Other custom hooks

 ### Benefit
 
|       Name                 | Description                                                   |
| ------------------------- | ------------------------------------------------------------- |
| ♻ **Reusability**         | Write once, reuse logic across multiple components.           |
| ✨ **Cleaner Code**        | Keeps components simple by separating logic.                  |
| 🧪 **Testability**        | Easier to test logic in isolation (without UI).               |
| 📦 **Abstraction**        | Hides complex logic behind a simple API.                      |
| 📁 **Organized Codebase** | Logic and UI are better separated, improving maintainability. |




