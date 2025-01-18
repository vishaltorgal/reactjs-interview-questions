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
