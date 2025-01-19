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
- Cross-Browser Compatibility: Synthetic events normalize behavior across browsers.
- Performance Optimization: Synthetic events are pooled for efficiency, which means the same event object is reused for multiple events.
- Consistent API: React provides the same interface regardless of the browser.

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


