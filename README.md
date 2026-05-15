# React JS Interview Questions (2025–2026)

### Table of Contents

1. [State in React](#1-state-in-react)
2. [Difference Between State and Props](#2-difference-between-state-and-props)
3. [Function Components vs Class Components](#3-function-components-vs-class-components)
4. [Lifecycle Phases in React](#4-lifecycle-phases-in-react)
5. [Stateful Components](#5-what-are-stateful-components)
6. [Controlled Components (forms)](#6-what-are-controlled-components-forms)
7. [Uncontrolled Components (forms) (useRef) vs createRef](#7-what-are-uncontrolled-components-forms-useref-vs-createref)
8. [Callback Function](#8-callback-function)
9. [Higher Order Components (HOC)](#9-what-are-higher-order-components-hoc)
10. [Callback vs Higher Order Component (HOC)](#10-callback-vs-higher-order-component-hoc)
11. [Pure Components](#11-pure-components)
12. [Synthetic Events](#12-synthetic-events)
13. [Key Prop in Lists](#13-key-prop-in-lists)
14. [Virtual DOM](#14-virtual-dom)
15. [React Fiber](#15-react-fiber)
16. [Fragments](#16-fragments)
17. [Ways to Optimize React Application](#17-ways-to-optimize-react-application)
18. [Context API](#18-context-api)
19. [What are Error Boundaries in React?](#19-what-are-error-boundaries-in-react)
20. [What is Lazy Loading and Suspense?](#20-what-is-lazy-loading-and-suspense)
21. [empty](#21-empty)
22. [What is code splitting in React?](#22-what-is-code-splitting-in-react)
23. [What is Prop Drilling in React?](#23-what-is-prop-drilling-in-react)
24. [empty](#24-empty)
25. [What background process on npm start](#25-what-background-process-on-npm-start)
26. [React design system libraries](#26-react-design-system-libraries)
27. [React vs Angular](#27-react-vs-angular)
28. [Modern React Patterns](#28-modern-react-patterns)
29. [React Query](#29-react-query)
30. [Ways to check performance of react app](#30-ways-to-check-performance-of-react-app)
31. [Protected Routes Login](#31-protected-routes-login)
32. [Role Based Restrictions](#32-role-based-restrictions)
33. [JWT Token Usage](#33-jwt-token-usage)
34. [Children](#34-children)
35. [Axios API Call](#35-axios-api-call)
36. [GraphQL](#36-graphql)
37. [React Folder Structure](#37-react-folder-structure)
38. [Pages vs Layout vs Components](#38-pages-vs-layout-vs-components)
39. [How to create a re-usable components](#39-how-to-create-a-re-usable-components)
40. [API layer](#40-api-layer)
41. [Debug](#41-debug)
42. [package.json vs package-lock.json](#42-packagejson-vs-package-lockjson)
43. [Security Issues](#43-security-issues)


    
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


<br>

## 3. **Function Components vs Class Components**

| Feature       | Functional Component | Class Component          |
| ------------- | -------------------- | ------------------------ |
| Syntax        | JavaScript function  | ES6 class                |
| State         | Managed using hooks  | Managed using this.state |
| Lifecycle     | useEffect hook       | Lifecycle methods        |
| Performance   | Lightweight          | Slightly heavier         |
| Current usage | Preferred            | Less used                |


<br>

## 4. Lifecycle Phases in React

React lifecycle has ***three*** main phases:

- `Mounting` – component is created and added to DOM
- `Updating` – component re-renders due to changes
- `Unmounting` – component is removed from DOM

### Table - React Lifecycle Phases

| Phase              | Lifecycle Method                    | When It Runs                    | Use Case                           |
| ------------------ | ----------------------------------- | ------------------------------- | ---------------------------------- |
| **Mounting**       | `constructor()`                     | When component is created       | Initialize state                   |
|                    | `static getDerivedStateFromProps()` | Before render                   | Update state from props            |
|                    | `render()`                          | Renders JSX to UI               | UI creation                        |
|                    | `componentDidMount()`               | After component is added to DOM | API calls, subscriptions           |
| **Updating**       | `static getDerivedStateFromProps()` | When props/state change         | Sync state with props              |
|                    | `shouldComponentUpdate()`           | Before re-render                | Performance optimization           |
|                    | `render()`                          | Re-render UI                    | Update UI                          |
|                    | `getSnapshotBeforeUpdate()`         | Before DOM update               | Capture DOM info (scroll position) |
|                    | `componentDidUpdate()`              | After update                    | API calls on update                |
| **Unmounting**     | `componentWillUnmount()`            | Before component removed        | Cleanup timers, listeners          |
| **Error Handling** | `static getDerivedStateFromError()` | When child throws error         | Show fallback UI                   |
|                    | `componentDidCatch()`               | After error occurs              | Log error                          |


### Example (Class Component)
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
<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/0f855e39-12e3-4274-812c-532e183e09b1" />


### Example (functional Component)

1️⃣ Mounting Phase

👉 When component is created and inserted into DOM.

`What happens:`
- Component renders for the first time
- DOM is created
- Effects run

```jsx
useEffect(() => {
  console.log("Component Mounted");
}, []);
```
Empty dependency array → runs only once → on mount.



2️⃣ Updating Phase

👉 When component re-renders because:

- State changes
- Props change

```jsx
useEffect(() => {
  console.log("Component Updated");
});
```
Runs after every render.

***Or:***
```jsx
useEffect(() => {
  console.log("Count changed");
}, [count]);
```
Runs only when count changes.

3️⃣ Unmounting Phase

👉 When component is removed from DOM.

```jsx
useEffect(() => {
  return () => {
    console.log("Component Unmounted");
  };
}, []);
```

The return function is the cleanup function.

### 🎯 Functional Component Mapping

| Class Lifecycle      | Hook Equivalent                     |
| -------------------- | ----------------------------------- |
| componentDidMount    | useEffect(() => {}, [])             |
| componentDidUpdate   | useEffect(() => {}, [deps])         |
| componentWillUnmount | useEffect(() => { return cleanup }) |


### 🎯 Simple Timeline

- Step 1: User hides component
- Step 2: React starts unmount
- Step 3: Cleanup runs
- Step 4: DOM removed
- Step 5: UI not visible

<br>

## 5. **What are stateful components?**

A stateful component is a component that uses/manages state.

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return <h1>{count}</h1>;
}
```

`Counter` is called a stateful component because it contains React state.

### Comparison with Stateless (Functional) Components
- `Stateful components` can modify and track their state over time.
- `Stateless components` (also called "dumb" components) do not manage their own state; they simply receive props from their parent component and render UI based on those props.

  <br>

## 6. **What are controlled components (forms)?**

A Controlled Component is a form element whose value is controlled by React state.

Controlled components in React are form elements like `<input>`, `<textarea>`, and `<select>` where the value is controlled by React's state. The form element's value is set by the state, and any changes to the input are handled through event handlers that update the state.

```jsx
import React, { useState } from "react";

function App() {
  const [value, setValue] = useState("");

  return (
    <>
      <input
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      <h1>{value}</h1>
    </>
  );
}

```

### Key Points
- The value of the input is tied to the text state.
- The onChange handler updates the state when the user types, keeping the input value in sync with the state.

<br>

## 7. **What are Uncontrolled Components (forms) (useRef) vs createRef**

***Uncontrolled components*** use DOM to store form values and refs like useRef (functional) or createRef (class) to access them without React controlling the input state.

### What is an Uncontrolled Component?

An uncontrolled component is a form element where:

- 👉 DOM stores and manages the value
- 👉 React does NOT track every change
- 👉 We access value only when needed using refs

### useRef (Functional Components)
useRef is used in functional components to access DOM elements.

```jsx
import React, { useRef } from "react";

function App() {
  const firstRef = useRef(null);
  const secondRef = useRef(null);

  function handleSubmit() {
    alert(
      `First: ${firstRef.current.value}, Second: ${secondRef.current.value}`
    );
  }

  return (
    <>
      <input ref={firstRef} type="text" />
      <input ref={secondRef} type="text" />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}

export default App;
```

### Key points (useRef)
- Used in functional components
- Stores reference to DOM element
- Does NOT cause re-render when value changes
- Value is accessed using ref.current.value
- Best for simple forms or direct DOM access
- 👉 DOM controls input, React just reads it when needed

### createRef (Class Components)
`createRef` is used in class components to create a reference to DOM elements.

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

### Key points (createRef)
- Used in class components
- Creates a new ref object
- Used to access DOM elements or class methods
- Does NOT cause re-render
- Mostly used in legacy code
- 👉 Works like useRef but for class components

| Feature           | createRef           | useRef                |
| ----------------- | ------------------- | --------------------- |
| Used in           | Class components    | Functional components |
| React version     | Older approach      | Modern approach       |
| Re-renders        | New ref each render | Same ref persists     |
| Best use          | Legacy code         | Modern React apps     |
| Causes re-render? | No                  | No                    |

<br>

## 8. **Callback Function**

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



### Passing values from child to parent

✅ Parent Component

```jsx
import React, { useState } from "react";
import Child from "./Child";

function Parent() {
  const [message, setMessage] = useState("");

  const receiveData = (data) => {
    setMessage(data);
  };

  return (
    <div>
      <h2>Message from Child: {message}</h2>

      <Child sendData={receiveData} />
    </div>
  );
}

export default Parent;
```

✅ Child Component
```jsx
import React from "react";

function Child({ sendData }) {
  return (
    <button onClick={() => sendData("Hello Parent!")}>
      Send Data
    </button>
  );
}

export default Child;
```

### Output

Initial screen (before click)
```jsx
Message from Child:
```

Updated screen (after click)
```jsx
Message from Child: Hello Parent!
```

<br>

## 9. **What are Higher-Order Components (HOC)?**

A Higher-Order Component (HOC) is a pattern in React that allows you to reuse component logic. It is a function that takes a component and returns a new component with added functionality.

### Key Points
- HOC is a function: It takes a component and returns a new component.
- It doesn’t modify the original component: Instead, it enhances or adds features to it.

### Example Usecase
- Authentication protection (Protected routes)
- Role based access control
- Logging / analytics wrapper
- Loading state handling
- Error handling (Error boundary style wrapper)
- Theming / styling injection
- Data fetching wrapper

### Step 1: Create HOC
```jsx
function withTitle(Component) {
  return function () {
    return (
      <div>
        <h2>This is a title added by HOC</h2>
        <Component />
      </div>
    );
  };
}
```

### Step 2: Create a simple component 
```jsx
function Hello() {
  return <p>Hello World</p>;
}
```

### Step 3: Wrap it using HOC
```jsx
const HelloWithTitle = withTitle(Hello);
```
<br>

## 10. **Callback vs. Higher-Order Component (HOC)**

| Feature          | Higher Order Component (HOC)                                        | Callback Function                                            |
| ---------------- | ------------------------------------------------------------------- | ------------------------------------------------------------ |
| Definition       | A function that takes a component and returns an enhanced component | A function passed from parent to child and executed by child |
| Purpose          | Reuse and enhance component logic                                   | Send data or trigger action from child to parent             |
| Direction        | Component → Component (wrapping)                                    | Child → Parent communication                                 |
| Used for         | Adding features like auth, logging, loading UI                      | Passing values or events                                     |
| Pattern type     | Component pattern                                                   | Function communication pattern                               |
| Data flow        | Wraps and modifies component                                        | Sends data upward                                            |
| Reusability      | High (logic reuse across components)                                | Medium (specific to parent-child relation)                   |
| Example use case | Add loader, auth check, role-based UI                               | Form input, button click handling                            |

<br>

## 11. **Pure Components**

A Pure Component is a React component that only re-renders when its props or state actually change.

If nothing changed, it skips re-render to improve performance.

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

    return <h1>{this.props.name}</h1>;
  }
}
```

### How it behaves

If you pass same props again:

```jsx
<MyComponent name="John" />
<MyComponent name="John" />
```
👉 It will NOT re-render second time


### ***Functional equivalent***
In modern React, we create pure components by wrapping a functional component in ***React.memo***

```jsx
import React from "react";

const MyComponent = ({ name }) => {
  console.log("Rendered");
  return <h1>{name}</h1>;
};

export default React.memo(MyComponent);
```

<br>


## 12. **synthetic events**

A Synthetic Event is React’s wrapper around native browser events like click, change, submit, etc.

Instead of using the browser event directly, React gives you a consistent event object.

### Key Points
- `Cross-Browser Compatibility`: Synthetic events normalize behavior across browsers.
- `Performance Optimization`: Synthetic events are pooled for efficiency, which means the same event object is reused for multiple events.
- `Consistent API`: React provides the same interface regardless of the browser.

```jsx
function Button() {
  function handleClick(event) {
    console.log(event);           // SyntheticEvent
    console.log(event.type);      // "click"
    console.log(event.target);    // DOM element
  }

  return <button onClick={handleClick}>Click Me</button>;
}
```
Here, event is not the native browser event directly. It is a React SyntheticEvent.

### What Is Inside a SyntheticEvent?

It has the same interface as native events:

- event.type
- event.target
- event.currentTarget
- event.preventDefault()
- event.stopPropagation()

### Real-Life Example
```jsx
function Input() {
  const handleChange = (e) => {
    console.log(e.target.value);
  };

  return <input onChange={handleChange} />;
}
```
<br>

## 13. **Key Prop in Lists**

The ***key prop*** helps React track which list items have changed, been added, or removed.

 ***Without key, React may***
- Re render unnecessary items
- Update the wrong components
- Cause UI bugs

Keys are special attributes in React used to uniquely identify elements in a list.

***Why Keys Are Important for Performance***
When a list changes, React:

- Compares previous Virtual DOM with new Virtual DOM
- Uses keys to identify which items changed, moved, or stayed the same
- Updates only the required DOM nodes

***Key Rules***
- Keys must be unique
- Keys must be stable
- Avoid using array index
- Use database IDs when possible
  
```jsx
const users = ["Vishal", "Amit", "Rahul"];

<ul>
  {users.map((name, index) => (
    <li key={name}>{name}</li>
  ))}
</ul>
```
<br>

## 14. **Virtual DOM**

<img width="681" height="240" alt="image" src="https://github.com/user-attachments/assets/947983c5-cf91-4867-b606-1119785bee26" />


### 🔄 How It Works (Step by Step)

- 1️⃣ React creates a Virtual DOM (JS object representation of UI)

- 2️⃣ When state changes, React creates a new Virtual DOM

- 3️⃣ React compares old Virtual DOM with new one. This process is called ***diffing***

- 4️⃣ Only the changed parts are updated in the real DOM. This process is called ***Reconciliation***


### How the Virtual DOM Works
- `Initial Render` : When the component is first rendered, the Virtual DOM creates a virtual representation of the DOM elements.
- `Diffing Algorithm` : React uses a diffing algorithm to compare the new virtual DOM tree with the previous one.
- `Efficient Updates` : React updates only the parts of the real DOM that have changed, minimizing direct DOM manipulations.


### We have 2 components c1 and c2. if something changed in c1 does c2 rerender or not?

### Case 1️⃣ C1 and C2 are siblings
```jsx
function App() {
  return (
    <>
      <C1 />
      <C2 />
    </>
  );
}
```
If state changes inside C1 only:
```jsx
function C1() {
  const [count, setCount] = useState(0);
}
```

- 👉 Only C1 re renders
- 👉 C2 does NOT re render
- Because C2 is independent.


### Case 2️⃣ State is in Parent

```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <>
      <C1 count={count} />
      <C2 />
    </>
  );
}
```

`Now when count changes:`

- 👉 App re renders
- 👉 C1 re renders
- 👉 C2 ALSO re renders
- Even if C2 does not use count

`Why?`
- Because parent re rendered, so all children render again.


### Case 3️⃣ Using React.memo
```jsx
const C2 = React.memo(() => {
  console.log("C2 render");
  return <div>C2</div>;
});
```

`Now:`

- If parent re renders
- But C2 props did not change
- 👉 C2 will NOT re render
- This prevents unnecessary renders.


### Simple Rule

If state changes inside component
- → Only that component re renders

If parent re renders
- → All children re render

Unless optimized with React.memo
<br>

## 15. **React Fiber**

React Fiber is the reconciliation engine introduced in React 16.

It is the internal algorithm that React uses to:
- Compare old virtual DOM with new virtual DOM
- Decide what needs to change
- Update the UI efficiently

***Before Fiber:***
Rendering was 
- Synchronous
- Blocking
- Could not be paused

***With Fiber:***
- Work can be paused, resumed, or cancelled
- High priority updates run first


### 🔥 Two Important Phases
1️⃣ Render Phase (Interruptible)

- Can pause
- Can resume
- Can cancel
- Builds Fiber tree

2️⃣ Commit Phase (Not Interruptible)

- Applies changes to DOM
- Must finish completely
- Very fast


### 🎯 Simple Example

`Imagine:`

- User is typing in input
- At the same time a big list is rendering

`With old React:`
- List rendering could block typing

`With Fiber:`
- Typing is high priority
- List rendering can pause
- Typing stays smooth

### 🔥 Key Concepts of Fiber
1️⃣ Incremental Rendering
- Break large rendering work into small chunks.

2️⃣ Priority Based Updates
- User interactions > background rendering.

3️⃣ Better Scheduling
- React decides best time to update UI.




## 16. **Fragments**

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

## 17. **Ways to optimize react application**

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

## 18. **Context API**

The ***Context API*** in React is used to share data globally across components without passing props manually at every level.

### Context.js
```jsx
import React, { createContext } from 'react';
export const UserContext = createContext();

const UserProvider = ({ children }) => {
  const user = { name: 'John Doe', id: 1 };
  
  return (
    <UserContext.Provider value={user}>
      {children}
    </UserContext.Provider>
  );
};

export default UserProvider;
```

### App.js
```jsx
import React from 'react';
import WelcomePage from './WelcomePage';
import UserProvider from './Context';

const App = () => {
  return (
    <UserProvider>
      <WelcomePage />
    </UserProvider>
  );
};

export default App;
```
### WelcomePage.js
```jsx
import React, { useContext } from 'react';
import { UserContext } from './Context';

const WelcomePage = () => {
  const { user } = useContext(UserContext);

  return (
    <div>
      <h1>Welcome User:</h1>
      <p>Name: {user.name} id: {user.id}</p>
    </div>
  );
};

export default WelcomePage;
```

### ***Key points***

- Avoids prop drilling
- Useful for global data
- Triggers re render when value changes

## Context API + useReducer

### reducer.js
```jsx
export const counterReducer = (state, action) => {
  switch (action.type) {

    case "INCREMENT":
      return { count: state.count + 1 };

    case "DECREMENT":
      return { count: state.count - 1 };

    default:
      return state;
  }
};
```

### CounterContext.js
```jsx
import { createContext, useReducer } from "react";
import { counterReducer } from "./reducer";

export const CounterContext = createContext();

export const CounterProvider = ({ children }) => {

  const [state, dispatch] = useReducer(counterReducer, { count: 0 });

  return (
    <CounterContext.Provider value={{ state, dispatch }}>
      {children}
    </CounterContext.Provider>
  );
};
```

### CounterDisplay.js
```jsx
import { useContext } from "react";
import { CounterContext } from "./CounterContext";

function CounterDisplay() {

  const { state } = useContext(CounterContext);

  return <h2>Count: {state.count}</h2>;
}

export default CounterDisplay;
```

### CounterButtons.js
```jsx
import { useContext } from "react";
import { CounterContext } from "./CounterContext";

function CounterButtons() {

  const { dispatch } = useContext(CounterContext);

  return (
    <div>

      <button onClick={() => dispatch({ type: "INCREMENT" })}>
        Increase
      </button>

      <button onClick={() => dispatch({ type: "DECREMENT" })}>
        Decrease
      </button>

    </div>
  );
}

export default CounterButtons;
```

### App.js
```jsx
import { CounterProvider } from "./CounterContext";
import CounterDisplay from "./CounterDisplay";
import CounterButtons from "./CounterButtons";

function App() {

  return (
    <CounterProvider>
      <CounterDisplay />
      <CounterButtons />
    </CounterProvider>
  );
}

export default App;
```
<br>

## 19. What are Error Boundaries in React?

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

### functional Components ErrorBoundary
```jsx
npm install react-error-boundary
```

```jsx
import { ErrorBoundary } from "react-error-boundary";

function ErrorFallback({ error }) {
  return (
    <div>
      <p>Something went wrong:</p>
      <pre>{error.message}</pre>
    </div>
  );
}

function App() {
  return (
    <ErrorBoundary FallbackComponent={ErrorFallback}>
      <MyComponent />
    </ErrorBoundary>
  );
}
```

### What Error Boundaries Catch

`They catch errors in:`

- ✔ Rendering
- ✔ Lifecycle methods
- ✔ Constructors

<br>

## 20. What is Lazy Loading and Suspense?

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


### 🏠 Example: E commerce Homepage
```jsx
import React, { useState, Suspense } from "react";

const Banner1 = React.lazy(() => import("./Banner1"));
const Banner2 = React.lazy(() => import("./Banner2"));
const Banner3 = React.lazy(() => import("./Banner3"));

function HomePage() {
  const [search, setSearch] = useState("");

  return (
    <div>
      <h1>My Store</h1>

      <input
        type="text"
        placeholder="Search products..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
      />

      <Suspense fallback={<div>Loading Banner1...</div>}>
        <Banner1 />
      </Suspense>

      <Suspense fallback={<div>Loading Banner2...</div>}>
        <Banner2 />
      </Suspense>

      <Suspense fallback={<div>Loading Banner3...</div>}>
        <Banner3 />
      </Suspense>

      <p>Searching for: {search}</p>
    </div>
  );
}

export default HomePage;
```

- ✔ Parallel loading
- ✔ Whichever finishes first renders first


⚠️ Important:
- If both banners are inside one Suspense
- The fallback shows until both components load


### 🔥 What Happens Internally

1️⃣ Homepage loads
- Header + Input render immediately

2️⃣ Banner is NOT loaded at first
- It starts loading in background

3️⃣ User starts typing

`React Fiber sees:`

- Typing = High priority
- Banner loading = Lower priority

- 👉 Typing stays smooth
- 👉 Banner continues loading without blocking

### Suspense does not make code load faster, but it:

- Prevents blocking the UI
- Shows meaningful loading states
- Allows splitting large bundles
- Improves first paint and user perception
- You can wrap specific components, not entire app

### 🧠 Why This Is Good

`Without Fiber and lazy loading:`
- Large banner JS could block main thread
- Typing might lag

`With Fiber:`
- React splits work
- Gives priority to user interaction

<br>

## 21. empty


## 22. What is code splitting in React?

`Code Splitting means:`

- 👉 Breaking your JavaScript bundle into smaller chunks
- 👉 Loading those chunks only when needed
- 👉 This improves performance and reduces initial load time.


***Types of Code Splitting***
| Type             | Description            |
| ---------------- | ---------------------- |
| Route based      | Split code per route   |
| Component based  | Split heavy components |
| Vendor splitting | Separate libraries     |

### ✅ Simple Example (Route Based Splitting)

```jsx
import React, { Suspense } from "react";

const About = React.lazy(() => import("./About"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <About />
    </Suspense>
  );
}
```

<br>

## 23. What is Prop Drilling in React?

Prop drilling is a situation in React where data is passed from a parent component to deeply nested child components through multiple intermediate components, even though those intermediate components do not need the data.

***Problems Caused by Prop Drilling***

- Unnecessary props in components
- Hard to maintain code
- Difficult to refactor

***How to Avoid Prop Drilling***

- Use Context API
- Use state management libraries like Redux
- Tightly coupled components

<br>

## 24. Empty



<br>

## 25. What background process on npm start

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

<br>

## 26. React design system libraries

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

## 27. React vs Angular

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

<br>

## 28. **Modern React Patterns**

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

<br>

## 29. **React Query**

React Query is used to fetch and manage server data easily.

### Setup Provider

```jsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Users />
    </QueryClientProvider>
  );
}
```
### Simple Example

```jsx
import { useQuery } from "@tanstack/react-query";

function Users() {
  const { data, isLoading, error } = useQuery({
    queryKey: ["users"],
    queryFn: async () => {
      const res = await fetch("https://jsonplaceholder.typicode.com/users");
      return res.json();
    }
  });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error...</p>;

  return (
    <ul>
      {data.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

### ✅ Advantages
1️⃣ Automatic Caching

If another component requests "users":
- No extra API call.
- Data comes from cache.

2️⃣ Background Refetch

`When:`
- User refocuses tab
- Internet reconnects
- Data refreshes automatically.

3️⃣ Built-in Loading & Error States

`You get:`
- isLoading
- error
- isFetching

No manual state needed.

4️⃣ Deduplication

If 5 components request same data:
- Only 1 network request happens.

### 🔥 When to Use React Query?

Use React Query when:
- Your app fetches data from APIs
- You need caching
- You need background updates
- You want less boilerplate
- You have pagination or infinite scroll

### 🔥 React Query vs useEffect

| useEffect             | React Query      |
| --------------------- | ---------------- |
| Manual state handling | Automatic        |
| No caching            | Built-in caching |
| More boilerplate      | Cleaner          |
| Harder scaling        | Scales well      |


## 30. Ways to check performance of react app

### 1️⃣ React DevTools Profiler

Use the Profiler tab in React DevTools.

To see the React DevTools Profiler, you first need to install the React Developer Tools browser extension. Then it will appear inside Chrome DevTools.

***What it shows:***

- Which components re-render
- How many times they re-render
- How long each render took
- Why component re-rendered

### 2️⃣ Chrome Performance Tab
Use Chrome DevTools Performance tab.

***What it shows:***

- CPU usage
- JavaScript execution time
- Paint time
- Layout shifts
- Memory usage

***Core Web Vitals Comparison***

| Metric                              | What it Measures                                | When it Happens                   | Good Value        |
| ----------------------------------- | ----------------------------------------------- | --------------------------------- | ----------------- |
| **LCP (Largest Contentful Paint)**  | Time to render the largest visible content      | Page loading                      | ≤ **2.5 seconds** |
| **CLS (Cumulative Layout Shift)**   | Visual stability (layout shifting unexpectedly) | During page load & render         | ≤ **0.1**         |
| **INP (Interaction to Next Paint)** | Responsiveness after user interaction           | After user clicks, taps, or types | ≤ **200 ms**      |

<img width="416" height="313" alt="image" src="https://github.com/user-attachments/assets/4e4a7e8a-9ab7-46e6-bedc-d6e4429f6a01" />


### 3️⃣ Lighthouse Report
Inside Chrome DevTools → Lighthouse tab.

***What it shows:***

- Performance score
- Accessibility score
- SEO score
- Best practices
- Suggestions to improve

<img width="415" height="325" alt="image" src="https://github.com/user-attachments/assets/816343ad-798c-42e9-9ce7-ca20d7b3ddbb" />


### 4️⃣ React Profiler API (Advanced)

React has built-in Profiler component:

```jsx
import { Profiler } from "react";

<Profiler id="App" onRender={(...args) => console.log(args)}>
  <App />
</Profiler>
```

***What it shows:***

- Slow components
- Expensive re-renders
- Whether memo is working
- Performance bottlenecks
 -Re-render frequency


### React performance table

| Method             | Tool                    | What It Checks                        | When To Use                    |
| ------------------ | ----------------------- | ------------------------------------- | ------------------------------ |
| React Profiler     | React Developer Tools   | Component re-renders, render time     | Debug slow components          |
| Chrome Performance | Google Chrome DevTools  | CPU usage, JS execution, paint time   | Detect blocking or heavy tasks |
| Lighthouse         | Lighthouse              | Performance score, SEO, accessibility | Optimize production app        |
| Why Did You Render | why-did-you-render      | Unnecessary re-renders                | Debug memo issues              |
| Bundle Analyzer    | webpack-bundle-analyzer | Bundle size, heavy dependencies       | Reduce app size                |
| Console Logging    | Browser console         | Count re-renders                      | Quick debugging                |


<br>

## 31. Protected Routes Login

### ✅ What This Achieves

 ✔ Logged in user can access
- /profile
- /settings

✔ Non logged in user
- Can only see homepage

If they try /profile → redirected to home
- ✔ Clean separation
- ✔ Reusable ProtectedRoute

### Folder Structure
```jsx
src/
 ├── App.js
 ├── auth/
 │     └── AuthContext.js
 ├── routes/
 │     └── ProtectedRoute.js
 └── pages/
       ├── Home.js
       ├── Profile.js
       └── Settings.js
```

### 1️⃣ Auth Context (Global Login State)
`📄 auth/AuthContext.js`

```jsx
import { createContext, useContext, useState } from "react";

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null); 
  // null = not logged in

  const login = () => {
    setUser({ id: 1, name: "Vishal" });
  };

  const logout = () => {
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  return useContext(AuthContext);
}

```

### 2️⃣ Protected Route
`📄 routes/ProtectedRoute.js`

```jsx
import { Navigate } from "react-router-dom";
import { useAuth } from "../auth/AuthContext";

function ProtectedRoute({ children }) {
  const { user } = useAuth();

  if (!user) {
    return <Navigate to="/" replace />;
  }

  return children;
}

export default ProtectedRoute;
```

### 3️⃣ Pages
`📄 pages/Home.js`

```jsx
import { useAuth } from "../auth/AuthContext";

function Home() {
  const { user, login, logout } = useAuth();

  return (
    <div>
      <h2>Home Page</h2>

      {user ? (
        <>
          <p>Welcome {user.name}</p>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <button onClick={login}>Login</button>
      )}
    </div>
  );
}

export default Home;
```

### 4️⃣ App.js
```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { AuthProvider } from "./auth/AuthContext";
import ProtectedRoute from "./routes/ProtectedRoute";

import Home from "./pages/Home";
import Profile from "./pages/Profile";
import Settings from "./pages/Settings";

function App() {
  return (
    <AuthProvider>
      <BrowserRouter>
        <Routes>

          <Route path="/" element={<Home />} />

          <Route
            path="/profile"
            element={
              <ProtectedRoute>
                <Profile />
              </ProtectedRoute>
            }
          />

          <Route
            path="/settings"
            element={
              <ProtectedRoute>
                <Settings />
              </ProtectedRoute>
            }
          />

        </Routes>
      </BrowserRouter>
    </AuthProvider>
  );
}

export default App;
```

### 📄 pages/Profile.js
```jsx
function Profile() {
  return <h2>Profile Page</h2>;
}

export default Profile;
```

### 📄 pages/Settings.js
```jsx
function Settings() {
  return <h2>Settings Page</h2>;
}

export default Settings;
```

<br>

## 32. Role Based Restrictions

### 🔄 How JWT Flow Works (Very Simple)

- 1️⃣ User logs in
- 2️⃣ Backend verifies credentials
- 3️⃣ Backend sends JWT
- 4️⃣ React stores JWT
- 5️⃣ React sends JWT in API calls
- 6️⃣ Backend verifies JWT

### ✅ Simple Role Protected Route
```jsx
import { Navigate } from "react-router-dom";

function RoleProtected({ role, children }) {
  const user = { role: "user" }; // change to "admin" to test

  if (user.role !== role) {
    return <Navigate to="/" replace />;
  }

  return children;
}
```

### ✅ Usage
```jsx
<Route
  path="/admin"
  element={
    <RoleProtected role="admin">
      <h2>Admin Page</h2>
    </RoleProtected>
  }
/>
```

### 🔎 What Happens

- If user.role === "admin" → page shows
- If not → redirected to home

## 33. JWT Token Usage

### Step 1: Login and Store Token
```jsx
const handleLogin = async () => {
  const res = await fetch("/login", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ email, password })
  });

  const data = await res.json();

  localStorage.setItem("token", data.token);
};
```

### Step 2: Send Token in API Call
```jsx
const token = localStorage.getItem("token");

fetch("/profile", {
  headers: {
    Authorization: `Bearer ${token}`
  }
});
```

### Step 3: Protect Route Using Token
```jsx
function ProtectedRoute({ children }) {
  const token = localStorage.getItem("token");

  if (!token) {
    return <Navigate to="/" />;
  }

  return children;
}
```

### 🕒 When Do We Use JWT in React?

- ✔ You have login system
- ✔ Backend needs to verify user identity
- ✔ You want protected APIs
- ✔ You want role based access

***JWT is used for authentication and authorization.***

### can we use jwt even we dont have login
`JWT is mainly used for:`

- Authentication
- Authorization
- Identifying a specific user
  
`If there is no login, then:`

- No user identity
- No role
- No protected data
- No need to verify user
- So JWT is unnecessary.

<br>

## 34. Children

In React, children is a special prop that represents the content placed inside a component tag.

### ✅ Simple Meaning

Whatever you write inside a component:
```jsx
<Card>
  <h2>Hello</h2>
</Card>
```

The <h2>Hello</h2> part becomes children.

### ✅ Real Usage Example: Layout Wrapper
```jsx
function Layout({ children }) {
  return (
    <>
      <header>Navbar</header>
      <main>{children}</main>
      <footer>Footer</footer>
    </>
  );
}
```

Usage

```jsx
<Layout>
  <Profile />
</Layout>
```

- Navbar and Footer stay same
- Profile is dynamic content (children)

<br>

## 35. Axios API Call

### Basic GET Request
```jsx
import axios from "axios";

const token = "your_jwt_token_here";

axios.get("https://api.example.com/users", {
  headers: {
    Authorization: `Bearer ${token}`
  }
})
.then((response) => {
  console.log(response.data);
})
.catch((error) => {
  console.log(error);
});
```

### ✔ What happens?

- axios.get() sends request
- .then() runs when success
- .catch() runs when error

  
### Using async/await (Cleaner)
```jsx
import axios from "axios";

async function fetchUsers() {
  const token = localStorage.getItem("token");

  try {
    const response = await axios.get(
      "https://api.example.com/users",
      {
        headers: {
          Authorization: `Bearer ${token}`
        }
      }
    );

    console.log(response.data);
  } catch (error) {
    console.log(error);
  }
}

fetchUsers();
```


### 📡 Axios Interceptor Basic Example
`An Axios interceptor lets you run code:`

- ✅ Before request is sent
- ✅ After response is received
- ✅ On error

`Mostly used for:`

- Attaching JWT token
- Handling 401 errors
- Logging
- Global error handling

### ✅ 1️⃣ Request Interceptor Example
Used to attach token automatically.

```jsx
import axios from "axios";

const api = axios.create({
  baseURL: "https://api.example.com",
});

api.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem("token");

    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }

    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

export default api;
```

### 🔹 What happens here?

`Before every API call:`

- Token is read from localStorage
- Added in headers
- Then request continues

### ✅ 2️⃣ Response Interceptor Example
Used to handle global errors like 401.

```jsx
api.interceptors.response.use(
  (response) => {
    return response;
  },
  (error) => {
    if (error.response?.status === 401) {
      console.log("Unauthorized. Redirect to login.");
      window.location.href = "/login";
    }

    return Promise.reject(error);
  }
);
```

### ✅ 3️⃣ How To Use
```jsx
import api from "./api";

api.get("/users")
   .then(res => console.log(res.data))
   .catch(err => console.log(err));
```

### 🧠 Real Life Flow

- User logs in → token saved in localStorage
- Every request → interceptor adds token
- If token expired → response interceptor catches 401 → redirect

<br>

## 36. GraphQL

### Setup Apollo Client

```jsx
import { ApolloClient, InMemoryCache } from "@apollo/client";

const client = new ApolloClient({
  uri: "https://example.com/graphql", // your GraphQL API
  cache: new InMemoryCache(),
});

export default client;
```

### Fetch Data in Page (SSR Example)
```jsx
// pages/index.js

import { gql } from "@apollo/client";
import client from "../lib/apollo";

export async function getServerSideProps() {
  const { data } = await client.query({
    query: gql`
      query {
        users {
          id
          name
        }
      }
    `,
  });

  return {
    props: {
      users: data.users,
    },
  };
}

export default function Home({ users }) {
  return (
    <div>
      <h1>User List</h1>
      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}
```

- SEO friendly ✅
- Single request ✅
- Only required fields fetched ✅

### 🎯 Why This Is Powerful

`Instead of:`
- Multiple REST calls

`You get:`
- Exact nested data in one query
- Clean structure

<br>

## 37. React Folder Structure

***Small Projects***

```jsx
src/
 ├── components/
 │    ├── Header.jsx
 │    ├── Footer.jsx
 │    └── Button.jsx
 │
 ├── pages/
 │    ├── Home.jsx
 │    └── About.jsx
 │
 ├── assets/
 │    ├── images/
 │    └── styles/
 │
 ├── utils/
 │    └── helpers.js
 │
 ├── App.jsx
 └── index.js
```

***Medium / Large Projects***

```jsx
src/
│
├── components/
│   ├── common/
│   │    ├── Button/
│   │    │    ├── Button.jsx
│   │    │    └── Button.module.scss
│   │
│   └── layout/
│        ├── Header/
│        └── Footer/
│
├── features/
│   ├── auth/
│   │    ├── Login.jsx
│   │    ├── Register.jsx
│   │    └── authSlice.js
│   │
│   ├── dashboard/
│   │    ├── Dashboard.jsx
│   │    └── Dashboard.scss
│
├── hooks/
│   ├── useAuth.js
│   └── useFetch.js
│
├── services/
│   └── api.js
│
├── store/
│   ├── store.js
│   └── rootReducer.js
│
├── utils/
│   ├── constants.js
│   └── helpers.js
│
├── styles/
│   └── global.scss
│
├── App.jsx
└── main.jsx
```

***Public pages, Authenticated pages, and Common components.***

```jsx
src/
│
├── pages/
│   │
│   ├── public/              (No login required)
│   │     ├── Home/
│   │     │     └── Home.jsx
│   │     │
│   │     └── InfoPage/
│   │           └── InfoPage.jsx
│   │
│   └── private/             (Login required)
│         ├── Settings/
│         │     └── Settings.jsx
│         │
│         └── Profile/
│               └── Profile.jsx
│
├── components/
│   │
│   ├── common/
│   │     ├── Header/
│   │     │     └── Header.jsx
│   │     │
│   │     └── Footer/
│   │           └── Footer.jsx
│   │
│   └── ui/                  (Reusable UI components)
│         ├── Button/
│         └── Modal/
│
├── layouts/
│     ├── PublicLayout.jsx
│     └── PrivateLayout.jsx
│
├── services/
│     └── api.js
│
├── hooks/
│
├── utils/
│
├── routes/
│     └── AppRoutes.jsx
│
├── App.jsx
└── index.js
```

<br>

## 38. Pages vs Layout vs Components

### Pages
Pages represent complete screens and are usually mapped to routes (URLs).

`Examples:`
- Home page
- Info page
- Profile page
- Settings page
- 

```jsx
function Home() {
  return <h1>Home Page</h1>;
}
```

### Layout

Layouts define the common page structure used by multiple pages.

`They usually contain:`
- Header
- Footer
- Sidebar
- bMain content wrapper

```jsx
import Header from "../components/Header";
import Footer from "../components/Footer";

function PublicLayout({ children }) {
  return (
    <>
      <Header />
      {children}
      <Footer />
    </>
  );
}

export default PublicLayout;
```

### Components

Components are reusable UI building blocks.

`Examples:`
- Button
- Card
- Header
- Footer
- Modal

```jsx
function Button({ label }) {
  return <button>{label}</button>;
}
```

### How They Work Together
```jsx
App
 └── Layout
       ├── Header (component)
       ├── Page (route)
       │     ├── Card (component)
       │     └── Button (component)
       └── Footer (component)
```

<br>

## 39. How to create a re-usable components

### Use Props
Reusable components should accept props instead of hardcoded values.

❌ Not reusable
```jsx
function Button() {
  return <button>Submit</button>;
}
```

✅ Reusable
```jsx
function Button({ label }) {
  return <button>{label}</button>;
}
```
***Usage:***
```jsx
<Button label="Submit" />
<Button label="Cancel" />
```

### Use Children for Flexible Content
Use children when content inside component changes.

Example:
```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}
```

Usage:
```jsx
<Card>
  <h2>Profile</h2>
  <p>User information</p>
</Card>
```

### Make Component Configurable
Allow customization using props.

Example:
```jsx
function Button({ label, type }) {
  return <button className={type}>{label}</button>;
}
```
Usage:
```jsx
<Button label="Save" type="primary" />
<Button label="Delete" type="danger" />
```

### Separate Logic and UI

Example:
```jsx
function Input({ value, onChange, placeholder }) {
  return (
    <input
      value={value}
      onChange={onChange}
      placeholder={placeholder}
    />
  );
}
```
Usage:
```jsx
<Input
  value={name}
  onChange={(e) => setName(e.target.value)}
  placeholder="Enter name"
/>
```

### Use Default Props

Provide default values.

```jsx
function Button({ label = "Click", type = "primary" }) {
  return <button className={type}>{label}</button>;
}
```

`Best Practices`

- ✅ Use props for customization
- ✅ Use children for flexible content
- ✅ Keep components small and focused
- ✅ Avoid hardcoding data
- ✅ Keep UI separate from business logic

<br>

## 40. API layer

API layer means a separate layer in the application responsible for handling all API calls (communication with the backend) instead of writing API calls directly inside components.

It helps keep UI and data fetching logic separated.

### Without API Layer (Bad Practice)

API call directly inside component:
```jsx
import axios from "axios";

function Users() {
  useEffect(() => {
    axios.get("/api/users").then(res => console.log(res.data));
  }, []);
}
```

`Problems:`
- Logic mixed with UI
- Hard to reuse
- Hard to maintain

### With API Layer (Best Practice)

***API Layer File***
```jsx
// services/userApi.js
import axios from "axios";

export const getUsers = () => {
  return axios.get("/api/users");
};
```

***Component***
```jsx
import { getUsers } from "../services/userApi";

function Users() {
  useEffect(() => {
    getUsers().then(res => console.log(res.data));
  }, []);
}
```

### Folder Structure
```jsx
src
 ├── components
 ├── pages
 ├── services
 │     └── userApi.js
 ├── utils
 └── App.jsx
```

<br>

## 41. Debug

### 1. Browser DevTools

```jsx
Right Click → Inspect
or
F12
```

| Tab      | Use            |
| -------- | -------------- |
| Console  | Errors & logs  |
| Network  | API requests   |
| Elements | HTML structure |
| Sources  | Debug JS       |


### 2. Using debugger

```jsx
function handleClick() {
  debugger;
  setCount(count + 1);
}
```

`When this line runs, the browser pauses and you can inspect:`

- variables
- state
- call stack

### 3. React Developer Tools

Install React DevTools extension.

`Components Tab`

***Shows:***
- component tree
- props
- state
- hooks

### 4. Debug API Calls

`Use Network tab to see:`
- request URL
- response data
- status codes

### 5. React Profiler (Performance Debugging)

`React DevTools → Profiler tab`

***Used to detect:***
- slow components
- unnecessary re-renders

### 6. Error Boundaries
Catch UI errors.

```jsx
class ErrorBoundary extends React.Component {
  componentDidCatch(error, info) {
    console.log(error, info);
  }

  render() {
    return this.props.children;
  }
}
```

### Debugging Tools Summary

| Method         | Purpose                  |
| -------------- | ------------------------ |
| console.log    | Quick debugging          |
| debugger       | Pause execution          |
| DevTools       | Inspect browser behavior |
| React DevTools | Inspect components       |
| Network tab    | Debug API                |
| React Profiler | Performance analysis     |

<br>

## 42. package.json vs package-lock.json

package.json defines project dependencies and configuration, while package-lock.json locks the exact versions of those dependencies to ensure consistent installations across environments.

### package.json
package.json is the main project configuration file.

`It contains:`
- project metadata
- dependencies
- scripts
- version information

```jsx
{
  "name": "my-react-app",
  "version": "1.0.0",
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build"
  },
  "dependencies": {
    "react": "^18.2.0",
    "axios": "^1.5.0"
  }
}
```

***Key Points***

| Feature  | package.json          |
| -------- | --------------------- |
| Purpose  | Project configuration |
| Contains | dependencies list     |
| Editable | Yes (developer edits) |
| Used for | installing packages   |


### package-lock.json
package-lock.json locks the exact versions of dependencies installed.

```jsx
"axios": {
  "version": "1.5.0",
  "resolved": "https://registry.npmjs.org/axios/-/axios-1.5.0.tgz",
  "integrity": "sha512..."
}
```
***Key Points***

| Feature      | package-lock.json               |
| ------------ | ------------------------------- |
| Purpose      | Locks exact dependency versions |
| Generated by | npm automatically               |
| Editable     | No                              |
| Ensures      | same install for everyone       |

### Simple Analogy

| File              | Analogy                      |
| ----------------- | ---------------------------- |
| package.json      | Shopping list                |
| package-lock.json | Actual bill with exact items |

<br>

## 43. Security Issues
`Common risks include:`

- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- Sensitive data exposure
- Insecure API calls
- Improper authentication handling

### What is XSS and how does React prevent it?
XSS (Cross-Site Scripting) happens when malicious scripts are injected into the application.

Example of risky code:
```jsx
<div dangerouslySetInnerHTML={{ __html: data }} />
```

***Best practice:***
- Avoid using it
- Sanitize data using libraries like DOMPurify

```jsx
import DOMPurify from "dompurify";

const cleanHTML = DOMPurify.sanitize(data);
```

### How to secure API calls in React?

- Use HTTPS
- Add authentication tokens
 -Avoid exposing sensitive data

### secrets not be stored in React code
React apps run in the browser, so users can inspect the code.

```jsx
const API_KEY = "123456";
```

Anyone can see it in DevTools.

`Solution:`
- Store secrets on the backend
- Use environment variables only for non-sensitive values.

### Prevent CSRF attacks

CSRF occurs when a malicious site sends requests using an authenticated user.

`Solutions:`
- CSRF tokens
- SameSite cookies
- Server validation

### Content Security Policy (CSP)
CSP is a browser security feature that prevents loading unauthorized scripts.

```jsx
Content-Security-Policy: script-src 'self'
```

### How to protect against dependency vulnerabilities?
React apps use many packages.

```jsx
npm audit
npm audit fix
```
