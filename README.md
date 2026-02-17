# React JS Interview Questions (2025–2026)

### Table of Contents

1. [State in React](#1-state-in-react)
2. [Difference Between State and Props](#2-difference-between-state-and-props)
3. [Higher Order Components (HOC)](#3-what-are-higher-order-components-hoc)
4. [Pure Components](#4-what-are-pure-components-in-react)
5. [Synthetic Events](#5-what-are-synthetic-events-in-react)
6. [Key Prop in Lists](#6-what-is-key-prop-and-what-is-the-benefit-of-using-it-in-arrays-of-elements)
7. [Virtual DOM](#7-what-is-virtual-dom)
8. [Controlled Components](#8-what-are-controlled-components)
9. [Uncontrolled Components](#9-what-are-uncontrolled-components)
10. [Fragments](#10-what-are-fragments)
11. [Stateful Components](#11-what-are-stateful-components)
12. [Function Components vs Class Components](#12-function-components-vs-class-components)
13. [Ways to Optimize React Application](#13-ways-to-optimize-react-application)
14. [useRef Hook](#14-useref)
15. [createRef](#15-createref)
16. [React Fiber](#16-what-is-react-fiber)
17. [Callback Function](#17-callback-function)
18. [Callback vs Higher Order Component (HOC)](#18-difference-callback-vs-higher-order-component-hoc)
19. [useReducer](#19-usereducer)
20. [Context API](#20-context-api)
21. [Custom Hooks](#21-custom-hook)
22. [Difference between useState and useReducer](#22-difference-between-usestate-and-usereducer)
23. [Difference between useEffect and useLayoutEffect](#23-difference-between-useeffect-and-uselayouteffect)
24. [Difference between useMemo and useCallback](#24-difference-between-usememo-and-usecallback)
25. [Difference between useRef and useState](#25-difference-between-useref-and-usestate)
26. [Difference between CSR and SSR](#26-difference-between-csr-and-ssr)
27. [Lifecycle Phases in React](#27-lifecycle-phases-in-react)
28. [What are Error Boundaries in React?](#28-what-are-error-boundaries-in-react)
29. [What is Reconciliation in React?](#29-what-is-reconciliation-in-react)
30. [What is Lazy Loading?](#30-what-is-lazy-loading)
31. [What is Suspense in React?](#31-what-is-suspense-in-react)
32. [What is code splitting in React?](#32-what-is-code-splitting-in-react)
33. [What is Prop Drilling in React?](#33-what-is-prop-drilling-in-react)
34. [Keys and Re-rendering in React?](#34-keys-and-re-rendering-in-react)
35. [Types of Hooks in React?](#35-types-of-hooks-in-react)
36. [useMemo](#36-usememo)
37. [useCallback](#37-usecallback)
38. [Redux](#38-redux)
39. [Difference between custom hook and components](#39-difference-between-custom-hook-and-components)
40. [What background process on npm start](#40-what-background-process-on-npm-start)
41. [React design system libraries](#41-react-design-system-libraries)
42. [React vs Angular](#42-react-vs-angular)
43. [useReducer vs Context API vs Redux](#43-usereducer-vs-context-api-vsredux)
44. [Modern React Patterns](#44-modern-react-patterns)

    
## 1. **State in React**

***State*** is a built in React object used to store dynamic data and re render the component when the data changes.

### Key Points
- State is mutable using setState or useState
- State changes trigger re rendering
- State is local to the component
- State should not be modified directly


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



## 2. **Difference Between State and Props**

| Feature    | Props (Properties)               | State                                      |
| ---------- | -------------------------------- | ------------------------------------------ |
| Definition | Data passed from parent to child | Data managed internally within a component |
| Mutability | Immutable for child              | Mutable                                    |
| Source     | External                         | Internal                                   |
| Update     | Cannot be updated by child       | Updated using setState or hooks            |
| Usage      | Component communication          | Dynamic behavior                           |
| Re render  | Changes trigger re render        | Changes trigger re render                  |




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

Pure Components in React are components that avoid unnecessary re renders by doing a shallow comparison of props and state.

### Key Points
- React automatically compares previous vs next props and state
- Uses shallow comparison
- If nothing changed, React skips re render



### ***Class component***

```jsx
import React, { PureComponent } from "react";

class MyComponent extends PureComponent {
  render() {
    console.log("Rendered");
    return <h1>Hello</h1>;
  }
}

```
### ***Functional equivalent***
In modern React, we create pure components by wrapping a functional component in ***React.memo***

```jsx
const MyComponent = React.memo(() => {
  console.log("Rendered");
  return <h1>Hello</h1>;
});
```
<br>

## 5. **What are synthetic events in React?**

A synthetic event is a cross browser wrapper around the browser’s native event.

### Key Points
- `Cross-Browser Compatibility`: Synthetic events normalize behavior across browsers.
- `Performance Optimization`: Synthetic events are pooled for efficiency, which means the same event object is reused for multiple events.
- `Consistent API`: React provides the same interface regardless of the browser.

```jsx
function Button() {
  function handleClick(e) {
    console.log(e);           // SyntheticEvent
    console.log(e.target);    // Works like native event
  }

  return <button onClick={handleClick}>Click me</button>;
}
```
<br>

## 6. **What is "key" prop and what is the benefit of using it in arrays of elements?**

The ***key prop*** helps React track which list items have changed, been added, or removed.

### ***Why key is important***
Without key, React may:
- Re render unnecessary items
- Update the wrong components
- Cause UI bugs

```jsx
const users = ["Vishal", "Amit", "Rahul"];

<ul>
  {users.map((name, index) => (
    <li key={name}>{name}</li>
  ))}
</ul>
```
<br>

## 7. **What is Virtual DOM?**

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

## 8. **What are controlled components?**

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

## 9. **What are Uncontrolled components?**

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



## 10. **What are fragments?**

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

## 11. **What are stateful components?**

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

## 12. **Function Components vs Class Components**

| Feature       | Functional Component | Class Component          |
| ------------- | -------------------- | ------------------------ |
| Syntax        | JavaScript function  | ES6 class                |
| State         | Managed using hooks  | Managed using this.state |
| Lifecycle     | useEffect hook       | Lifecycle methods        |
| Performance   | Lightweight          | Slightly heavier         |
| Current usage | Preferred            | Less used                |


<br>

## 13. **Ways to optimize react application**

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

## 14. **useRef**

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

## 15. **createRef**

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

## 16. **What is React Fiber?**

React Fiber is the internal architecture React uses to break rendering work into units and prioritize updates.

***Before Fiber:***
- Rendering was synchronous
- Large updates could block the UI

***With Fiber:***
- Work can be paused, resumed, or cancelled
- High priority updates run first

<br>

## 17. **Callback Function**

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

## 18. **Difference Callback vs. Higher-Order Component (HOC)**

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

## 19. **useReducer**

***useReducer*** is a React Hook used for state management when state logic is complex or depends on previous state.

***Syntax***
```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```
***Example***
simple useReducer pattern for a form with many fields.

`When a form has:`
- name
- email
- password
- confirmPassword
- etc

Using multiple useState becomes messy. So we use useReducer.

### 🧠 Why useReducer for forms?
```jsx
const [name, setName] = useState("")
const [email, setEmail] = useState("")
const [password, setPassword] = useState("")
```
We manage everything in one state object.

### ✅ Simple Example: Registration Form

Step 1️⃣ Define initial state
```jsx
const initialState = {
  name: "",
  email: "",
  password: ""
};
```

Step 2️⃣ Create reducer function
```jsx
function formReducer(state, action) {
  switch (action.type) {
    case "UPDATE_FIELD":
      return {
        ...state,
        [action.field]: action.value
      };

    case "RESET":
      return initialState;

    default:
      return state;
  }
}
```

Step 3️⃣ Use in Component
```jsx
import React, { useReducer } from "react";

export default function SignupForm() {
  const [state, dispatch] = useReducer(formReducer, initialState);

  function handleChange(e) {
    dispatch({
      type: "UPDATE_FIELD",
      field: e.target.name,
      value: e.target.value
    });
  }

  function handleSubmit(e) {
    e.preventDefault();
    console.log(state);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="name"
        value={state.name}
        onChange={handleChange}
        placeholder="Name"
      />

      <input
        name="email"
        value={state.email}
        onChange={handleChange}
        placeholder="Email"
      />

      <input
        name="password"
        type="password"
        value={state.password}
        onChange={handleChange}
        placeholder="Password"
      />

      <button type="submit">Submit</button>
      <button type="button" onClick={() => dispatch({ type: "RESET" })}>
        Reset
      </button>
    </form>
  );
}
```

### 🔥 Why This Is Better

- ✔ One state object
- ✔ Centralized logic
- ✔ Easy to scale
- ✔ Easy to add validation
- ✔ Cleaner for complex forms


| useState         | useReducer           |
| ---------------- | -------------------- |
| Simple state     | Complex state        |
| Direct updates   | Action based updates |
| Less boilerplate | More predictable     |


<br>

## 20. **Context API**

The ***Context API*** in React is used to share data globally across components without passing props manually at every level.

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

### ***Create Context***
```jsx
import { createContext } from "react";

const ThemeContext = createContext();
```
### ***Provide Context***
```jsx
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Dashboard />
    </ThemeContext.Provider>
  );
}
```
### ***Consume Context***
```jsx
import { useContext } from "react";

function Dashboard() {
  const theme = useContext(ThemeContext);
  return <p>{theme}</p>;  //<p>dark</p>
}

```
### ***Key points***

- Avoids prop drilling
- Useful for global data
- Triggers re render when value changes

<br>

## 21. **custom hook**

- A custom hook is a reusable JavaScript function that uses React hooks and starts with the word ***use***.
- It helps you share logic between components without repeating code.
  
### ***Custom Hook**
```jsx
import { useState } from "react";

function useCounter() {
  const [count, setCount] = useState(0);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);

  return { count, increment, decrement };
}

```

### ***Use the Hook in a Component***
```jsx
function Counter() {
  const { count, increment, decrement } = useCounter();

  return (
    <>
      <p>{count}</p>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </>
  );
}
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

***Difference from Component***

| Custom Hook            | Component            |
| ---------------------- | -------------------- |
| Reuses logic           | Renders UI           |
| No JSX return          | Returns JSX          |
| Used inside components | Used in UI tree      |
| Starts with `use`      | Normal function name |

<br>

## 22. Difference between useState and useReducer

| Feature      | useState             | useReducer             |
| ------------ | -------------------- | ---------------------- |
| Complexity   | Simple state         | Complex state logic    |
| Update style | Direct update        | Action based update    |
| Readability  | Less for large state | Better for large state |
| Use case     | Counters, toggles    | Forms, complex flows   |

<br>

## 23. Difference between useEffect and useLayoutEffect

| Feature        | useEffect    | useLayoutEffect      |
| -------------- | ------------ | -------------------- |
| Execution time | After paint  | Before paint         |
| UI blocking    | Non blocking | Blocking             |
| Performance    | Better       | Can hurt performance |
| Use case       | API calls    | DOM measurements     |

## 24. Difference between useMemo and useCallback

| Feature      | useMemo                | useCallback                      |
| ------------ | ---------------------- | -------------------------------- |
| Purpose      | Memoizes value         | Memoizes function                |
| Return value | Cached value           | Cached function                  |
| Usage        | Expensive calculations | Prevent re creation of functions |

## 25. Difference between useRef and useState

| Feature    | useRef             | useState             |
| ---------- | ------------------ | -------------------- |
| Re render  | Does not re render | Re renders component |
| Mutability | Mutable            | Immutable            |
| Use case   | DOM access         | UI updates           |

## 26. Difference between CSR and SSR

| Feature      | CSR     | SSR    |
| ------------ | ------- | ------ |
| Rendering    | Browser | Server |
| SEO          | Poor    | Good   |
| Initial load | Slow    | Fast   |

## 27. Lifecycle Phases in React

React lifecycle has ***three*** main phases:

`Mounting` – component is created and added to DOM
`Updating` – component re-renders due to changes
`Unmounting` – component is removed from DOM

***Example (Class Component)***

```jsx
class Demo extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  componentDidMount() {
    console.log("Mounted");
  }

  componentDidUpdate() {
    console.log("Updated");
  }

  componentWillUnmount() {
    console.log("Unmounted");
  }

  render() {
    return <h1>{this.state.count}</h1>;
  }
}

```

***Lifecycle Methods vs Hooks***

| Class Lifecycle      | Hook Equivalent                     |
| -------------------- | ----------------------------------- |
| componentDidMount    | useEffect(() => {}, [])             |
| componentDidUpdate   | useEffect(() => {}, [deps])         |
| componentWillUnmount | useEffect(() => { return cleanup }) |

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/0f855e39-12e3-4274-812c-532e183e09b1" />


## 28. What are Error Boundaries in React?

Error Boundaries are React components that catch JavaScript errors in:

- Child component rendering
- Lifecycle methods
- Constructors of child components

They prevent the entire app from crashing and display a fallback UI instead.

```jsx
function App() {
  const [count, setCount] = React.useState(0);

  return (
    <ErrorBoundary>
      <BuggyComponent count={count} />
      <button onClick={() => setCount(count + 1)}>+</button>
    </ErrorBoundary>
  );
}

```

- Error boundaries do not catch event handler errors
- Only class components can be error boundaries
- You can wrap specific components, not the entire app always

## 29. What is Reconciliation in React?

***Reconciliation*** is the process React uses to update the UI efficiently when state or props change.

Instead of updating the entire DOM, React:

- Creates a new Virtual DOM
- Compares it with the previous Virtual DOM
- Updates only the changed parts in the real DOM

## 30. What is Lazy Loading?

 Lazy loading in React is a performance optimization technique where components are loaded only when they are needed, instead of loading all components at the initial application load.

This reduces:

- Initial bundle size
- Page load time
- Memory usage

and improves application performance.

***React uses:***

- `React.lazy()` to load components dynamically
- `Suspense` to show a fallback UI while loading

***Why use it?***

Without lazy loading, a user visiting your "Home" page has to wait for the browser to download the code for the "Settings," "Admin," and "Profile" pages too. This leads to:

- Large Bundle Sizes: Slower initial page loads.
- Wasted Bandwidth: Users download code they might never use.
- Higher Bounce Rates: Especially on mobile devices or slow networks.

```jsx
import React, { Suspense, lazy } from "react";

const Profile = lazy(() => import("./Profile"));

function App() {
  return (
    <Suspense fallback={<h3>Loading...</h3>}>
      <Profile />
    </Suspense>
  );
}

export default App;

```
## 31. What is Suspense in React?

Suspense is a React component that lets you pause rendering of part of the UI and show a fallback UI while waiting for something to load, most commonly lazy loaded components.

Suspense does not make code load faster, but it:

- Prevents blocking the UI
- Shows meaningful loading states
- Allows splitting large bundles
- Improves first paint and user perception
- You can wrap specific components, not entire app

## 32. What is code splitting in React?

Code splitting in React is a performance optimization technique where a large JavaScript bundle is split into smaller chunks, and only the required code is loaded when needed.

This helps:

- Reduce initial bundle size
- Improve first page load time
- Improve application performance

***Types of Code Splitting***
| Type             | Description            |
| ---------------- | ---------------------- |
| Route based      | Split code per route   |
| Component based  | Split heavy components |
| Vendor splitting | Separate libraries     |


## 33. What is Prop Drilling in React?

Prop drilling is a situation in React where data is passed from a parent component to deeply nested child components through multiple intermediate components, even though those intermediate components do not need the data.

***Problems Caused by Prop Drilling***

- Unnecessary props in components
- Hard to maintain code
- Difficult to refactor

***How to Avoid Prop Drilling***

- Use Context API
- Use state management libraries like Redux
- Tightly coupled components

## 34. Keys and Re-rendering in React?

Keys are special attributes in React used to uniquely identify elements in a list.

***Why Keys Are Important for Performance***
When a list changes, React:

- Compares previous Virtual DOM with new Virtual DOM
- Uses keys to identify which items changed, moved, or stayed the same
- Updates only the required DOM nodes

  Without proper keys, React may re-render more elements than necessary.

***Key Rules***

- Keys must be unique
- Keys must be stable
- Avoid using array index
- Use database IDs when possible

## 35. Types of Hooks in React?

***Basic Hooks***
| Hook       | Purpose             | Use Case                 | Example                                 |
| ---------- | ------------------- | ------------------------ | --------------------------------------- |
| useState   | Manage local state  | Form inputs, counters    | `const [count, setCount] = useState(0)` |
| useEffect  | Handle side effects | API calls, subscriptions | `useEffect(() => fetchData(), [])`      |
| useContext | Consume context     | Theme, auth, language    | `const theme = useContext(ThemeCtx)`    |

***Additional Hooks***
| Hook        | Purpose                         | Use Case                 | Example                                               |
| ----------- | ------------------------------- | ------------------------ | ----------------------------------------------------- |
| useRef      | Persist value without re-render | Focus input, timers      | `const inputRef = useRef(null)`                       |
| useReducer  | Complex state logic             | Forms, state machines    | `const [state, dispatch] = useReducer(reducer, init)` |
| useCallback | Memoize function                | Prevent child re-renders | `useCallback(fn, [])`                                 |
| useMemo     | Memoize value                   | Expensive calculations   | `useMemo(calc, [deps])`                               |

***Layout & Effect Hooks***
| Hook               | Purpose                     | Use Case            | Example                            |
| ------------------ | --------------------------- | ------------------- | ---------------------------------- |
| useLayoutEffect    | DOM-read/write before paint | Measure layout      | `useLayoutEffect(() => {}, [])`    |
| useInsertionEffect | Inject styles before paint  | CSS-in-JS libraries | `useInsertionEffect(() => {}, [])` |

***Use Case Mapping***
| Scenario            | Best Hook             |
| ------------------- | --------------------- |
| Input handling      | useState              |
| API call            | useEffect             |
| Avoid re-render     | useMemo / useCallback |
| Share data globally | useContext            |
| Heavy UI update     | useTransition         |
| Access DOM          | useRef                |
| Complex logic       | useReducer            |

<br>

## 36. useMemo

***useMemo*** returns a cached value and recomputes it only when its dependencies change.

```jsx
import { useMemo, useState } from "react";

function App() {
  const [count, setCount] = useState(0);
  const [number, setNumber] = useState(5);

  const squared = useMemo(() => {
    console.log("Calculating...");
    return number * number;
  }, [number]);

  return (
    <>
      <p>Square: {squared}</p>
      <button onClick={() => setCount(count + 1)}>Re render</button>
    </>
  );
}
```

🔥  ***When to use useMemo***
- ✔ Prevent unnecessary re computations
- ✔ Expensive calculations
- ✔ Large array filtering
- ✔ Sorting big data
- ✔ Complex derived values
- ✔ Performance optimization needed

🚫 ***When NOT To Use useMemo***
- ❌ For small simple calculations
- ❌ Just to “optimize everything”
- ❌ Without performance issue
- Because useMemo itself has some overhead.

🏋️ ***Real Life Example***

**You have:**
- 10,000 employee records
- You calculate total yearly salary
- This calculation is heavy.

**Now suppose:**
*You also have a button that changes theme color.*
- When theme changes:
- Component re-renders.

**Without useMemo:**
- Total salary recalculates again ❌
- Even though salary data did not change.

**With useMemo:**
- React remembers the previous calculation ✅
- It only recalculates if employee data changes.

  
## 37. useCallback

***useCallback*** remembers a function, so it is not recreated on every render.

```jsx
import React, { useState, useCallback } from "react";

function App() {
  const [count, setCount] = useState(0);

  const sayHello = useCallback(() => {
    console.log("Hello");
  }, []);

  return (
    <>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <button onClick={sayHello}>Say Hello</button>
    </>
  );
}

export default App;
```
- useCallback remembers a function so it is not recreated on every re render.
- React normally creates functions again and again.
- useCallback stops that and keeps the same function.


🔥 When To Use useCallback
- ✔ Passing functions to child components
- ✔ Child component is wrapped with React.memo
- ✔ Function is inside dependency array of useEffect
- ✔ Performance optimization is needed


🚫 When NOT To Use It
- ❌ If function is not passed to children
- ❌ If app is small
- ❌ If there is no performance issue
- ❌ For every function blindly
  
<br>

## 38. Redux

***Redux*** is a state management library used to manage global application state in a predictable way.
- Redux stores the entire app state in one central store and updates it using actions and reducers.

***Core concepts***
- Store → where state lives
- Action → what happened
- Reducer → how state changes

***Store***
```jsx
import { createStore } from "redux";
const store = createStore(counterReducer);
```
***Action***
```jsx
const increment = { type: "INCREMENT" };
```
***Reducer***
```jsx
function counterReducer(state = 0, action) {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    default:
      return state;
  }
}
```

***Using Redux in React***
```jsx
import { Provider, useSelector, useDispatch } from "react-redux";

function Counter() {
  const count = useSelector(state => state);
  const dispatch = useDispatch();

  return (
    <>
      <p>{count}</p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>
        Increase
      </button>
    </>
  );
}
```

<br>

## 39. Difference between custom hook and components

| Aspect          | Component                  | Custom Hook             |
| --------------- | -------------------------- | ----------------------- |
| Purpose         | Builds and renders UI      | Reuses stateful logic   |
| Return value    | JSX                        | Data, state, functions  |
| Naming          | Starts with Capital letter | Must start with `use`   |
| Can use hooks   | Yes                        | Yes                     |
| Can return JSX  | Yes                        | No                      |
| Reusability     | Reused by rendering        | Reused by calling       |
| Concern         | UI + behavior              | Behavior only           |
| Example usage   | `<UserProfile />`          | `useUser()`             |
| Best used when  | You need to show something | You need to share logic |
| React treats as | Renderable element         | Logic abstraction       |

<br>

## 40. What background process on npm start

***When you run:***
- npm looks into package.json
- Finds this line: "start": "react-scripts start"
- So npm runs react-scripts
- react-scripts then starts all the background processes

***Those background processes are started by react-scripts 👇***
- Webpack dev server starts
- Babel transpiles JSX and modern JS
- File watcher listens for code changes
- Hot reload refreshes the browser
- ESLint runs checks in the background
- Environment variables are loaded

***Key difference in one line***

- ***npm start*** → just a trigger (command runner)
- ***react-scripts*** → does the actual work in background

## 41. React design system libraries

***React design system libraries*** are pre-built, reusable UI components that follow a consistent design language across an application or across multiple apps.

They solve one big problem:
👉 UI consistency + speed + accessibility

***What’s inside a design system library***
- Buttons
- Inputs
- Modals
- Tables
- Cards
- Typography
- Colors and spacing tokens
- Icons
- Accessibility rules
- Theming support

***Example in React***
Instead of writing buttons everywhere:

```jsx
<Button variant="primary" size="md">
  Save
</Button>
```

***Popular React design system libraries***
- Material UI (MUI) – Google Material Design
- Ant Design – Enterprise dashboards
- Chakra UI – Simple and accessible
- Radix UI – Headless components

***How it fits with microfrontends***
- Different teams
- Different repos
- Same look and feel

<br>

## 42. React vs Angular

| Aspect           | React                               | Angular                         | Which is better & why                   |
| ---------------- | ----------------------------------- | ------------------------------- | --------------------------------------- |
| Type             | UI library                          | Full-fledged framework          | Angular if you want everything built-in |
| Learning curve   | Easier, flexible                    | Steep, opinionated              | React is better for quick learning      |
| Language         | JavaScript / TypeScript             | TypeScript only                 | React is more flexible                  |
| Architecture     | Unopinionated                       | Opinionated (MVC-like)          | Angular suits large teams               |
| State management | External libraries (Redux, Zustand) | Built-in (RxJS, services)       | Angular for structured state            |
| Performance      | Very fast with Virtual DOM          | Very fast with change detection | React slightly better for dynamic UI    |
| Boilerplate      | Minimal                             | Heavy                           | React is better for simplicity          |
| Tooling          | Choose what you want                | CLI, routing, forms built-in    | Angular for consistency                 |
| Two-way binding  | No                                  | Yes                             | Angular easier for form-heavy apps      |
| Mobile support   | React Native                        | Ionic / NativeScript            | React has stronger ecosystem            |
| Community        | Massive                             | Large but smaller than React    | React wins                              |
| Use cases        | SPAs, dashboards, startups          | Enterprise-scale apps           | Depends on project size                 |


## React

***Use React when:***
- You want flexibility in architecture
- Project is small to medium
- Team size is small
- You want faster development
- You are building highly interactive UI
- You plan to use microfrontends
- You want a huge ecosystem and hiring pool
- You prefer choosing your own tools (router, state, etc.)
- Dashboards
- Admin panels
- Startups
- Consumer apps

## Angular

***Use Angular when:***
- Project is large and complex
- Multiple teams are working together
- You need strict structure and consistency
- App is form-heavy
- Enterprise-level standards are required
- You want everything built-in
- Long-term maintainability is critical
- Banking apps
- Government portals
- Enterprise dashboards


## 43. useReducer vs Context API vs redux

🎬 Imagine You Are Managing a Restaurant

***We’ll compare:***
- useReducer
- Context API
- Redux


## 1️⃣ useReducer
🍳 `Kitchen Manager`

*Inside the kitchen:*

***Many things can happen to one order:****

- Add item
- Remove item
- Change quantity
- Apply discount
- Cancel order

*All these actions affect one order state.*

***You need rules:***
- Cannot cook if ingredients are out
- Cannot apply discount twice
- Cannot cancel after serving

So the kitchen manager handles all order decisions properly.

👉 **That kitchen manager = useReducer**

***When to use:***
- One feature
- Complex logic
- Many actions changing the same state
- Clear decision rules needed

## 2️⃣ Context API
📢 `Restaurant Announcement System`

*Now imagine:*

***The restaurant has information everyone needs:***
- Today’s special dish
- Restaurant closing time
- Discount day
- Chef name

*Instead of telling each waiter individually, you make an announcement.*

*Everyone can access that info easily.*

👉 **That announcement system = Context API**

***When to use:***
- Theme
- Logged-in user
- Language
- Small global settings
- Data that many components need

***Important:***
- Context only shares data.
- It does not manage complex logic.


## 3️⃣ Redux
🏢 `Restaurant Franchise Headquarters`

***Now imagine:***

*You own 200 restaurant branches across the country.*

***You need:***
- Centralized order tracking
- Inventory management
- Employee management
- Payment systems
- Analytics
- Logging
- Strict rules
- Audit tracking

*You cannot manage this casually.*

***You need:***
- Structured flow
- Predictable updates
- Middleware
- Debugging tools
- Scalable architecture

👉 **That headquarters system = Redux**


## 44. **Modern React Patterns**

1️⃣ Functional Components + Hooks (Instead of Classes)

2️⃣ Custom Hooks (Logic Reuse Pattern)

3️⃣ Component Composition (Instead of Inheritance)

Example
```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}
```

Usage
```jsx
<Card>
  <h2>Title</h2>
  <p>Description</p>
</Card>
```
This makes components flexible and reusable.

4️⃣ Controlled Components (Forms Pattern)

5️⃣ Lifting State Up
- When multiple components need same data, move state to parent.

` Real life example:`
- Two siblings need same user data → parent holds state → passes as props.

6️⃣ Context API for Global State
When prop drilling becomes messy:
- Theme
- Auth
- Language
- User

7️⃣ useReducer Pattern (Complex State)
- Forms with many fields
- Shopping cart
- Complex UI state

8️⃣ Memoization (Performance Optimization)
`useMemo`
Avoid expensive recalculation.

`useCallback`
Avoid function recreation.

`React.memo`
Prevent unnecessary re-render of child.

9️⃣ Server Components
- No useEffect needed.
- Runs on server.
- This is modern full stack React pattern.

 🔟 Suspense & Lazy Loading

 1️⃣1️⃣ Colocation Pattern
 Keep:

- Component
- Styles
- Tests
- Hooks

In same folder.

```jsx
UserCard/
  UserCard.jsx
  UserCard.module.css
  useUser.js
```

🚀 Modern React Architecture Summary
| Concern       | Modern Approach                 |
| ------------- | ------------------------------- |
| State         | Hooks                           |
| Reuse logic   | Custom hooks                    |
| Global state  | Context / Redux                 |
| Performance   | Memoization                     |
| Data fetching | React Query / Server components |
| Code split    | Lazy + Suspense                 |
| Structure     | Colocation                      |
